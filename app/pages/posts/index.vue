<template>
  <section class="container posts-page">
    <el-card>
      <div slot="header" class="clearfix">
        <span>新着投稿</span>
      </div>
      <el-table
        :data="showPosts"
        style="width: 100%" 
        @row-click="handleClick"
        class="table"
      >
        <el-table-column prop="title" label="タイトル"></el-table-column>
        <el-table-column prop="user.id" label="投稿者" width="180"></el-table-column>
        <el-table-column prop="created_at" label="投稿日時" width="240"></el-table-column>
      </el-table>
    </el-card>
  </section>
</template>

<script>
import moment from '~/plugins/moment'
import { mapGetters } from 'vuex'

// Element UI table
// https://element.eleme.io/#/en-US/component/table
export default {
  async asyncData({ store }) {
    await store.dispatch('posts/fetchPosts')
  },
  computed: {
    showPosts() {
      // https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/map
      // map() メソッドは、与えられた関数を配列のすべての要素に対して呼び出し、その結果からなる新しい配列を生成します。
      return this.posts.map( post => {
        post.created_at = moment(post.created_at).format('YYYY/MM/DD HH:mm:ss')
        return post
      })
    },
    ...mapGetters('posts', ['posts'])
  },
  methods: {
    handleClick(post) {
      this.$router.push(`/posts/${post.id}`)
    }
  }
  
}
</script>

<style>
.post-page .el-table__row {
  cursor: pointer;
}
</style>
