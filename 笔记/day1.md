1)要求
1.1：每一天老师书写代码务必三遍
1.2:node + webpack + VScode + 谷歌浏览器 + git
1.3:数组的方法 + promise + await + async + 模块化........

2)脚手架使用
2: vue init webpack 项目的名字
3|4：vue create 项目名称
脚手架目录:public + assets 文件夹区别
node_modules:放置项目依赖的地方
public:一般放置一些共用的静态资源，打包上线的时候，public 文件夹里面资源原封不动打包到 dist 文件夹里面
src：程序员源代码文件夹
-----assets 文件夹：经常放置一些静态资源（图片），assets 文件夹里面资源 webpack 会进行打包为一个模块（js 文件夹里面）
-----components 文件夹:一般放置非路由组件（或者项目共用的组件）
App.vue 唯一的根组件
main.js 入口文件【程序最先执行的文件】
babel.config.js:babel 配置文件
package.json：看到项目描述、项目依赖、项目运行指令
README.md:项目说明文件

3)脚手架下载下来的项目稍微配置一下
3.1:浏览器自动打开
在 package.json 文件中
"scripts": {
"serve": "vue-cli-service serve --open",
"build": "vue-cli-service build",
"lint": "vue-cli-service lint"
},

3.2 关闭 eslint 校验工具
创建 vue.config.js 文件：需要对外暴露
module.exports = {
lintOnSave:false,
}
3.3 src 文件夹的别名的设置
因为项目大的时候 src（源代码文件夹）：里面目录会很多，找文件不方便，设置 src 文件夹的别名的好处，找文件会方便一些
创建 jsconfig.json 文件
{
"compilerOptions": {
"baseUrl": "./",
"paths": {
"@/_": [
"src/_"
]
}
},
"exclude": [
"node_modules",
"dist"
]
}

4:项目上传 GIT
微信小程序实战课的时候，会带着大家玩耍的
注意:前面基础课程当中，创建分支、处理冲突等等
https://gitee.com/jch1011/shangpinhui_0607.git

5）路由的配置
vue-router
路由分为 KV

node 平台（并非语言）
对于后台而言:K 即为 URL 地址 V 即为相应的中间件
http://localhost:8080/0607
app.get("/0607",(res,req)=>{
res.send('我是祖国的老花骨朵');
});

前端路由:
K 即为 URL（网络资源定位符）
V 即为相应的路由组件

5.1 路由的一个分析
确定项目结构顺序:上中下 -----只有中间部分的 V 在发生变化，中间部分应该使用的是路由组件
2 个非路由组件|四个路由组件
两个非路由组件：Header 、Footer
路由组件:Home、Search、Login（没有底部的 Footer 组件，带有二维码的）、Register（没有底部的 Footer 组件，带二维码的）

5.2 安装路由
cnpm install --save vue-router
--save:可以让你安装的依赖，在 package.json 文件当中进行记录
5.3 创建路由组件【一般放在 views|pages 文件夹】
5.4 配置路由，配置完四个路由组件

6)创建非路由组件（2 个：Header、Footer）

非路由组件使用分为几步:
第一步：定义
第二步：引入
第三步：注册
第四步:使用

非路由组件的结构的搭建：
前台项目的结构与样式不需要自己写的，老师准备好了
辉洪老师静态页面：
结构 + 样式 +图片资源

项目采用的 less 样式,浏览器不识别 less 语法，需要一些 loader 进行处理，把 less 语法转换为 CSS 语法

1：安装 less less-loader@5
切记 less-loader 安装 5 版本的，不要安装在最新版本，安装最新版本 less-loader 会报错，报的错误 setOption 函数未定义

2:需要在 style 标签的身上加上 lang="less",不添加样式不生效

7)路由的跳转
路由的跳转就两种形式：声明式导航（router-link：务必要有 to 属性）
编程式导航 push||replace
编程式导航更好用：因为可以书写自己的业务逻辑

面试题：v-show 与 v-if 区别?
v-show:通过样式 display 控制
v-if：通过元素上树与下树进行操作
面试题:开发项目的时候，优化手段有哪些?
1:v-show|v-if
2:按需加载 8)首页|搜索底部是有 Footer 组件，而登录注册是没有 Footer 组件
Footer 组件显示|隐藏，选择 v-show|v-if
路由元信息

9）路由传参
params 参数：路由需要占位，程序就崩了，属于 URL 当中一部分
query 参数：路由不需要占位，写法类似于 ajax 当中 query 参数

路由传递参数先关面试题
1:路由传递参数（对象写法）path 是否可以结合 params 参数一起使用?
不可以：不能这样书写，程序会崩掉

2:如何指定 params 参数可传可不传?
如果路由要求传递 params（有占位符/search:keyword），而没有传递，路径（URL）会出现问题
如果想使参数可传可不传，可以在占位符后加？（/search:keyword?）

3:params 参数可以传递也可以不传递，但是如果传递是空串，如何解决？
使用 undefined 空串也会导致路径问题
this.$router.push({ name: 'search', params: { keyword: ''||undefined }, query: { k: this.keyword.toUpperCase() } })

4: 路由组件能不能传递 props 数据?
可以 有三种写法
① 布尔值写法 只能传 params 参数 在路由组件中加入 props 属性
/router:
{
name: "register",
path: "/register",
component: Register,
meta: { show: false },
props: true,
},
pages/search:
export default {
name: "component_name",
props: ['keyword'],
data () {
return {
};
}
}
② 对象写法 额外给路由组件传递一些 props
/router:
{
name: "register",
path: "/register",
component: Register,
meta: { show: false },
props: {a:1,b:2},
},
③ 函数写法：可以 params 传参，query 传参，通过 props 传递给路由组件
/router:
{
name: "register",
path: "/register",
component: Register,
meta: { show: false },
props: ($route)=>{
    return {keyword:$route.params.keyword, k:$route.query.k}
}
},
