---
layout: post

title: Vue axios 读取api.github.com展示用户信息

cover: /img/cover/github_hero.svg

tags: ['Vue', 'axios']
---



### 前言

> 本文是基于[Vue axios 读取api.github.com展示用户信息](https://blog.liantao.me/VueRep)功能原理的简单介绍，由于初学Vue有太多的不懂，导致数据展示以及Vue data数据的提取和传递造成了巨大的阻碍，在这里分享一些过程。
> 
> 
> 
> Vue作为一个没有入侵性的框架，并不限制你使用ajax框架。  
> 使用了Vue后，ajax部分你可以做如下选择： 
> 
> 1.使用JS原生XHR接口  
> 
> 2.引入JQuery或者Zepto 使用$.ajax();  
> 
> 3.使用Vue官方推荐的[axios](https://github.com/axios/axios)
> 
> 4.Vue的github上提供了[vue-resource](https://github.com/vuejs/vue-resource)插件 ：  
> 
> 5.使用[fetch.js](https://github.com/github/fetch)  
> 
> 6.自己封装一个ajax库



### 首先，`axios`是什么?

`axios` 是基于 promise 的 HTTP 客户端，用于页面和后台数据的网络交互。

github地址：[传送门](https://github.com/axios/axios)



### 为什么要用`axios`？

开源、独立

它是**[Vue的官方推荐](https://cn.vuejs.org/v2/cookbook/using-axios-to-consume-apis.html)**



### 使用方法(参考axios文档)



~~~html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
~~~



### 本文中axios的使用实例：

~~~javascript
                    axios

                        .get("https://api.github.com/users/"+this.username)
                        .then(function(response) {
                            app.result = response.data;
                            console.log("succeed",app.result);
                        })
                        .catch(error => {
                            console.log(error);
                            this.errored = true;
                        })
                        .finally(() => this.loading = false);
~~~



### api.github.com是什么？

一个github官方提供的接口。可以在这详细了解：[GitHub REST API v3](https://developer.github.com/v3/)

这里用的：[接口](https://api.github.com/users/)



### 主角Vue，介绍该[页面](https://blog.liantao.me/VueRep)使用Vue展示数据遇到的一些困难及解决方法



1. 由于Vue这个[特性](https://cn.vuejs.org/v2/guide/reactivity.html)的存在，导致从接口获取到的`json`数据无法直接赋值给Vue的·data·属性，所以我们得在`data`里提前声明一个`result`：



**data声明：**

~~~javascript
data:{

      result:[],

      },
~~~

**赋值**

~~~javascript
app.result = response.data;
~~~



2. 通过获取到data里的value图片地址，添加到`<img>`标签的`src=""`的地址栏中，从而实现图片展示，我第一反应是使用`{{ data.url }}`的形式传入，但是`{{}}`写在引号里就不管用了，所以：

   ```javascript
   <img v-bind:src="result.avatar_url">
   ```

   需要使用Vue的v-bind指令绑定data里的属性，result.avatar_url就是**github api**中用户头像的图片地址。

   

3. 使用 v-for 展示所有数据：

   

   ~~~javascript
       <!-- {{result}} -->
                       <dl class="dl-horizontal"  v-for="(value, key) in result">
                           <dt>{{key||"无"}}</dt>
                           <dd>{{value||"无"}}</dd>
                       </dl>
   ~~~

   值得注意的是，(value, key)的顺序。





### 项目源码：[github repository](https://github.com/Famine-Life/VueRep)



#### what？懒得拿？行吧！

~~~javascript
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>Vue axios 读取api.github.com展示用户信息</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- bootstrap -->
    <link href="https://cdn.bootcss.com/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <h1 style="text-align:center;">Vue axios 读取api.github.com展示用户信息</h1>
    <hr>
    <div id="app">
       <div  style="width:800px;margin:0 auto">
            <form  class="form-inline" id="search" @submit.prevent="onSubmit">
                <div class="form-group">
                    <label class="sr-only" for="exampleInputAmount">Famine-life</label>
                    <div class="input-group">
                        <div class="input-group-addon">输入github用户名：</div>
                        <input class="form-control"  placeholder="famine-life"  id="username" type="text" v-model="username">
                    </div>    
                    <button class="btn btn-primary" id="btn">获取用户信息</button>
                </div>
            </form>
            <div id="show_area">
                <div class="alert alert-success" role="alert">information of {{username}}</div>
                <div class="row">
                    <div class="col-sm-12">
                        <div class="thumbnail">
                        <!-- v-bind加载图片 -->
                        <img v-bind:src="result.avatar_url">
                        <div class="caption">
                            <ul class="list-group">
                                <li class="list-group-item list-group-item-info">常用信息展示栏</li>
                                <li class="list-group-item list-group-item-success">用户名：{{result.login}}</li>
                                <li class="list-group-item list-group-item-info">介绍：{{result.bio}}</li>
                                <li class="list-group-item list-group-item-warning">博客：{{result.blog}}</li>
                                <li class="list-group-item list-group-item-danger">姓名：{{result.name}}</li>
                                <li class="list-group-item list-group-item-success">地址：{{result.location}}</li>
                                <li class="list-group-item list-group-item-info">followers：{{result.followers}}</li>
                                <li class="list-group-item list-group-item-warning">following：{{result.following}}</li>
                            </ul>
                            <p><a href="#" class="btn btn-primary" role="button" @click="onShow">{{show_btn_value}}</a></p>
                        </div>
                        </div>
                    </div>
                </div>
                <div  class="thumbnail" v-if="isShow">
                    <!-- {{result}} -->
                    <dl class="dl-horizontal"  v-for="(value, key) in result">
                        <dt>{{key||"无"}}</dt>
                        <dd>{{value||"无"}}</dd>
                    </dl>
                </div>
            </div>
        </div>
   </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17-beta.0/vue.js"></script>
    <!-- jq看着用 -->
    <script src="https://cdn.bootcss.com/jquery/3.3.1/jquery.js"></script> 
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script>
         var app = new Vue({
            el: '#app',
            data:{
                    username:null,
                    result:[],
                    isShow:false,
                    show_btn_value:"展示完整信息"
            },
            methods:{
                onShow:function(){
                    if(!this.isShow){
                        this.isShow = true;
                        this.show_btn_value ="隐藏下面信息";
                    }else{
                        this.isShow = false;
                        this.show_btn_value="展示完整信息";
                    }
                },
                onSubmit:function(){
                    axios
                        .get("https://api.github.com/users/"+this.username)
                        .then(function(response) {
                            app.result = response.data;
                            console.log("succeed",app.result);
                        })
                        .catch(error => {
                            console.log(error);
                            this.errored = true;
                        })
                        .finally(() => this.loading = false);

                    /**jQuery写法
                    //jQuery.ajax( url [, settings ] )
                    $.ajax({url:"https://api.github.com/users/"+this.username,
                            method:"get",
                            data:{
                                username:"hello",
                                password:"null"
                            },
                            success: function(data){
                                console.log("succeed:",data);
                                app.result=data;
                                console.log("输出vue的data",app.result);
                            },
                            error: function(){
                                console.log("error");
                            }
                    });
                    */
                },
            }
                            
        });


    </script>
</body>
</html>
~~~



**END**












