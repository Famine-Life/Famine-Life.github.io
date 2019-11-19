---
layout: post
title: [vue-cli 配置vue项目环境笔记]
cover: /img/cover/light-bulb.jpg
tags: ['vue','vue-cli']
---
> 笔记本很久没有更新node了，结果这次配置环境，竟然一波三折

## Node,npm版本太久，导致webpack, vue-cli安装失败
 - 解决办法：更新[node.js](https://nodejs.org/en/), 
 - 更新npm命令：`npm intall -g npm`

## 接下来就是一帆风顺的时刻，安装webpack:
 - 命令：`npm intall webpack -g`

## 安装 vue-cli 脚手架
 - `npm install --global vue-cli`
 - 安装完成，`vue -V`可以查看`vue`版本(V是大写)
## 新建文件夹 test，使用vue-cli构建一个vue项目
 - 执行命令 `vue init webpack test`
**接下来，会被询问一系列的操作，如下：**

 1. ? Project name lnews
 2. ? Project description A Vue.js project
 3. ? Author 看着黎明丶庆幸 <xanwidtf@foxmail.com>
 4. ? Vue build standalone
 5. ? Install vue-router? Yes
 6. ? Use ESLint to lint your code? Yes? Pick an ESLint preset Standard
 7. ? Set up unit tests Yes
 8. ? Pick a test runner jest
 9. ? Setup e2e tests with Nightwatch? Yes
 10. ? Should we run `npm install` for you after the project has been created? (recommended) npm

最后，经过漫长的等待，安装完毕：
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcyMDE4LmNuYmxvZ3MuY29tL2Jsb2cvMTQxMTY2Mi8yMDE5MTEvMTQxMTY2Mi0yMDE5MTExOTIxNTgzMjE2NC04MDQ3MTM5NTgucG5n?x-oss-process=image/format,png)

**如图所示，`cd Lnews`进入项目文件夹，`npm run dev`运行项目**
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcyMDE4LmNuYmxvZ3MuY29tL2Jsb2cvMTQxMTY2Mi8yMDE5MTEvMTQxMTY2Mi0yMDE5MTExOTIyMDAwOTQ5Ny00MTcxNzk1NDcucG5n?x-oss-process=image/format,png)

## 浏览器输入：localhost:8080 查看效果
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcyMDE4LmNuYmxvZ3MuY29tL2Jsb2cvMTQxMTY2Mi8yMDE5MTEvMTQxMTY2Mi0yMDE5MTExOTIyMDExMDQwMS0yMDEwODEzODk4LnBuZw?x-oss-process=image/format,png)

END

    

