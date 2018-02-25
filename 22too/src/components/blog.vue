<template>
  <div id="bloglist">
    <h1>22too blog</h1>
    <a> written by {{ author }} </a>
    <div v-for="blog in blog_lists">
 
      <p>
        {{blog.title}}
        {{blog.date}}
      <div  v-html="blog.content_html">
      </div>
      </p>
     </div>
  
  </div>
</template>

<script type="text/javascript">
import config from "../config"
export default {
  data() {
    return {
      author: "22too",
      articles: [],
      blog_lists: []
    };
  },
  mounted: function() {
    this.$http
      .get(
        config.host+"api/index",
        {},
        {
          headers: {},
          emulateJSON: true
        }
      )
      .then(
        function(response) {
          // 这里是处理正确的回调
          this.blog_lists = response.body.blogs;
          // this.articles = response.data["subjects"] 也可以
        },
        function(response) {
          // 这里是处理错误的回调
          console.log(response);
        }
      );
  }
};
</script>

<style>

</style>


