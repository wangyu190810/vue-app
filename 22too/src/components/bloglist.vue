<template>
  <div id="bloglist">
    <h1>22too blog</h1>
    <a> written by {{ author }} </a>
    <div v-for="blog in blog_lists">
 
      <p>
        {{blog.title}}
        {{blog.date}}
      <div  v-html="blog.content_html" class="blog_content">
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

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
.blog_content
{
position:absolute;
right:100px;
width:300px;
background-color:#b0e0e6;
}

</style>


