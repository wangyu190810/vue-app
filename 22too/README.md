# y

> y

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).


#*更新数组时候注意使用*


    # 使用对象整体替换，使得重新初始化
    this.show_comments_flag = Object.assign({},this.show_comments_flag,data)
    
    # 这个方式也可以，但是我没有成功
    this.$set(this.show_comments_flag,chouti_id,falg)

    # 这样的直接赋值，vue无法检测，导致的结果就是数据在打印日志时候，变更了。但是vue展示数据不变。
    this.show_comments_flag[chouti_id] = falg

[上述问题参考blog](https://www.jianshu.com/p/34de360d6035)