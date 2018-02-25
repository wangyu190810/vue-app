<template>
  <div id="chouti">
    <div v-for="chouti_data in chouti_lists">
      <div id = "content">   
          <div id = "title">
            {{chouti_data.content.title}}
          </div>
          <div id= "createtime">
            发表时间:{{timestamp_to_date(chouti_data.content.createtime)}}
          </div>
          <!-- 
            vue bind href 不需要带括号，可以直接使用属性。
           -->
          <div id = "origurl">
            <a v-bind:href="chouti_data.content.url" >
              源地址链接
            </a>
          </div>
          
      </div>
      
      <button v-on:click="show_comments(chouti_data.id)">
        <div v-if="show_comments_flag[chouti_data.id]">
          
            关闭评论
        </div>
        <div v-else>
        展示评论
        </div>
         
      </button>
      <div v-if="show_comments_flag[chouti_data.id]==true">
        <div v-for ="comments in chouti_data.comments">
          <p>{{comments.nick}}
            发表时间:{{timestamp_to_date(comments.createTime)}}
          </p>
          {{comments.content}}
          {{comments.ups}}
        </div>
      </div>
    </div>
  
  </div>
</template>

<script type="text/javascript">
import config from "../config";
import timestamp_to_date from "../utils/DateTime";
export default {
  data() {
    return {
      chouti_lists: [],
      show_comments_flag:{
      },
      init_flag:false,
    };
  },
  methods: {
    timestamp_to_date: function(timestamp) {
      var a = new Date(timestamp / 1000);
      var year = a.getFullYear();
      var month = a.getMonth();
      var date = a.getDate();
      var hour = a.getHours();
      var min = a.getMinutes();
      var sec = a.getSeconds();
      var time =
        year + " " + month + " " + date + " " + hour + ":" + min + ":" + sec;
      return time;
    },
    show_comments:function(chouti_id){
        // console.log(""+chouti_id)
        // chouti_id = ""+chouti_id
        // this.show_comments_flag[chouti_id] = true
        var falg; 
        if (this.show_comments_flag[chouti_id] == false){
           falg = true
        }else if (this.show_comments_flag[chouti_id] == undefined){
          falg = true
        }else{
          falg = false
        }
        var data = this.show_comments_flag[chouti_id] = falg

        this.show_comments_flag = Object.assign({},this.show_comments_flag,data)
        // this.$set(this.show_comments_flag,chouti_id,falg)
        // console.log(this.show_comments_flag[chouti_id])
        // console.log(this.show_comments_flag)
    }
  },
  mounted: function() {
    console.log(config.other_host.tools + "spider/chouti/index");
    this.$http
      .get(
        config.other_host.tools + "spider/chouti/index",
        {},
        {
          headers: {},
          emulateJSON: true
        }
      )
      .then(
        function(response) {
          // 这里是处理正确的回调
          console.log(response);
          this.chouti_lists = response.body;
          if (this.init_flag==false){
            this.chouti_lists.forEach(data => {
                this.show_comments_flag[data.id] = false
            });
            this.init_flag==true
          }
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
#chouti {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
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
.blog_content {
  position: absolute;
  right: 100px;
  width: 300px;
  background-color: #b0e0e6;
}
#title {
  text-align: center;
  background-color: #2fc9dd;
}
#createtime {
  text-align: center;
  background-color: #12c9dd;
}
#origurl {
  text-align: center;
  background-color: #12591d;
}
#content {
  /* position:absolute; */
  /* text-align: center; */
  right: 400px;
  width: 300px;
  position:relative;
  left:40%
}
.comments {
}
</style>


