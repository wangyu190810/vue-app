<template>
  <div id="app">
    <!-- <img src="./assets/logo.png">
    <h1>{{ msg }}</h1>
    <h2>{{ lang }}</h2> -->
    <bloglist></bloglist>
    <chouti></chouti>
  </div>
</template>

// <script>
// import bloglist from "./components/bloglist.vue"
// export default {
//   name: 'app',
//   data () {
//     return {
//       msg: 'Welcome to Your Vue.js App',
//       lang:"py,php,cpp,c"
//     }
//   },
//    components: {bloglist }
// }
// </script>

<script>
import chouti from "./components/chouti.vue"
export default {
  name: 'app',
  data () {
    return {
      msg: "asdf",
      lang:"py,php,cpp,c"
    }
  },
   components: {chouti }
}
</script>


<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // text-align: center;
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
</style>
