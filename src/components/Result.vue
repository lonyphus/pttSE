<template>

  <div>
    <p class="mt-5" v-if="route=='Account' || route=='ViewRecords'">{{ input }} 之發文紀錄</p>
    <p class="mt-5" v-else-if="route=='Keyword'">{{ input }} 的相關推文</p>

    <table id="result" class="table table-striped">
      <thead>
        <tr v-if="route=='Account' || route=='ViewRecords'">
          <th v-for="i in accountHead" :key="i"> {{ i }} </th>
        </tr>
        <tr v-else-if="route=='Keyword'">
          <th v-for="i in keywordHead" :key="i"> {{ i }} </th>
        </tr>
      </thead>
  

      <tbody v-if="route=='Account' || route=='ViewRecords'">
        <tr v-for="item in arr" :key="item._id">
          <td>{{ item._source.board }}</td>
          <td>{{ new Date(Number(item._source.date) * 1000).toLocaleString().split(" ")[0] }}</td>
          <td><a target="_blank" :href="item._source.article_url">{{ item._source.article_title }}</a> </td>
          <td>{{ item._source.comment_tag }} : {{ item._source.content }}</td>
        </tr>
      </tbody>

      <tbody v-else-if="route=='Keyword'">
        <tr v-for="item in arr" :key="item._id">
          <td>{{ item._source.user_id }}</td>
          <td>{{ item._source.board }}</td>
          <td>{{ new Date(Number(item._source.date) * 1000).toLocaleString().split(" ")[0] }}</td>
          <td><a target="_blank" :href="item._source.article_url">{{ item._source.article_title }}</a> </td>
          <td>{{ item._source.comment_tag }} : {{ item._source.content }}</td>
        </tr>
      </tbody>

    </table>
  </div>

</template>

<style lang="scss" scoped>

</style>



<script>
  export default {
    name: "Result",
    data(){
      return {
        accountHead: ['看板', '日期', '標題', '類型'],
        keywordHead: ['作者帳號', '看板', '日期', '標題', '類型']
      }
    },
    computed: {
      route: function(){ return this.$route.name },
    },
    props: {
      arr: Array,
      input: String,
    },
  }
  
</script>