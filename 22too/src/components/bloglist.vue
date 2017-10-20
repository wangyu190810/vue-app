<template>
  <div id="bloglist">
    <h1>22too blog</h1>
    <a> written by {{ author }} </a>
    <div v-for="article in articles" class="text item">
        {{article.title}}
      </div>   
  </div>
</template>

<script type="text/javascript">
export default {
  data() {
    return {
      author: "22too",
      articles: []
    };
  }
};
</script>

<style>

</style>


