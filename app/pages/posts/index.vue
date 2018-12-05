<template>
  <section class="container posts-page">
    <el-card>
      <div slot="header" class="clearfix">
        <span>新着投稿</span>
      </div>
      <el-table
        :data="showPosts"
        style="width: 100%"
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
// Element UI table
// https://element.eleme.io/#/en-US/component/table
export default {
  async asyncData({ store }) {
    await store.dispatch('posts/fetchPosts')
  },
  computed: {
    showPosts() {
      return [
        {
          id: '001',
          title: 'How to development Nuxt.js Application',
          body: 'Lorem ipsum sit amet ...',
          created_at: '20018/10/30 12:00:00',
          user: {
            id: 'hiropy0123'
          }
        },
        {
          id: '002',
          title: 'Deployment Nuxt.js Application to Heroku',
          body: 'Lorem ipsum sit amet ...',
          created_at: '20018/10/30 13:00:00',
          user: {
            id: 'hiropy0123'
          }
        },
        {
          id: '003',
          title: 'Deployment Nuxt.js Application to Heroku',
          body: 'Lorem ipsum sit amet ...',
          created_at: '20018/10/30 14:00:00',
          user: {
            id: 'hiropy0123'
          }
        }
      ]
    }
  }
  
}
</script>

<style>
.post-page .el-table__row {
  cursor: pointer;
}
</style>
