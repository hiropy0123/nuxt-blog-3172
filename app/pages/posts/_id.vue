<template>
  <section class="container posts-page">
    <div style="flex: 1">
      <el-card v-if="post">
        <div slot="header" class="clearfix">
          <h2>{{ post.title }}</h2>
          <small>by {{ post.user.id }}</small>
        </div>
        <p>{{ post.body }}</p>
        <p class="text-right">{{ post.created_at | time }}</p>
      </el-card>
      <p>
        <nuxt-link to="/posts">&lt; 投稿一覧へ戻る</nuxt-link>
      </p>
    </div>
  </section>
</template>

<script>
import moment from '~/plugins/moment'
import { mapGetters, mapActions } from 'vuex'

export default {
  async asyncData({ store, route, error }) {
    const { id } = route.params

    if (store.getters['posts/posts'].find( p => p.id === id )) { // Array.prototype.find() 配列の要素に指定されたテスト関数を適用していき、テストを満たす最初の要素の 値 を返します。見付からない場合は undefined を返します。
      // ストアのidとurlから取得したidが一致する場合
      // すでにストアにデータがある
      return
    }
    // URLから判断したIDがストアにない場合
    try {
      // firebaseから記事1件取得してストアに追加
      await store.dispatch('posts/fetchPost', { id })
      if ( !(store.getters['posts/posts'].find( p => p.id === this.$route.params.id )) ) {
        // firebaseから再度取得した上で、投稿のURLと同じIDが見つからない場合
        throw new Error('post not found')
      }
    } catch (e) {
      // firebaseにアクセスして、IDが見つからない、またはアクセスできない場合
      error({ statusCode: 404 })
    }
  },
  computed: {
    post() {
      return this.posts.find(p => p.id === this.$route.params.id)
    },
    ...mapGetters('posts', ['posts'])
  },
  filters: {
    time(val) {
      return moment(val).format('YYYY/MM/DD HH:mm:ss')
    }
  }
}
</script>

<style>
.posts-page .el-table__row {
  cursor: pointer;
}
</style>
