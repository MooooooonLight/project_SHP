常见错误:
1:项目阶段，左侧菜单目录，只能有项目文件夹
2：单词错误
3：路由理解
KV：K--->URL V---->相应的组件
配置路由：
------路由组件
-----router--->index.js
import Vue from 'vue';
import VueRouter from 'vue-router';
//使用插件
Vue.use(VueRouter);
//对外暴露 VueRouter 类的实例
export default new VueRouter({
routes:[
{
path:'/home',
component:Home
}
]
})
------main.js 配置项不能瞎写

$router:进行编程式导航的路由跳转
this.$router.push|this.$router.replace
$route:可以获取路由的信息|参数
this.$route.path
this.$route.params|query
this.$route.meta

1)编程式导航路由跳转到当前路由(参数不变), 多次执行会抛出 NavigationDuplicated 的警告错误?
注意:编程式导航（push|replace）才会有这种情况的异常，声明式导航是没有这种问题，因为声明式导航内部已经解决这种问题。
这种异常，对于程序没有任何影响的。
为什么会出现这种现象:
由于 vue-router 最新版本 3.5.2，引入了 promise，当传递参数多次且重复，会抛出异常，因此出现上面现象,
第一种解决方案：是给 push 函数，传入相应的成功的回调与失败的回调
第一种解决方案可以暂时解决当前问题，但是以后再用 push|replace 编程式导航还是会出现类似现象，因此我们需要从‘根’治病；
第二种解决方法参照代码 重写 push 方法

2)将 Home 组件的静态组件拆分
2.1 静态页面（样式）
2.2 拆分静态组件
2.3 发请求获取服务器数据进行展示
2.4 开发动态业务
拆分组件：结构+样式+图片资源
一共要拆分为七个组件
三级联动模块可以注册为全局模块，只需注册一次可以在项目任意地方使用

3)axios 二次封装
AJAX:客户端可以'悄悄的'向服务器端发请求，在页面没有刷新的情况下，实现页面的局部更新。
XMLHttpRequest、$、fetch、axios
跨域:如果多次请求协议、域名、端口号有不同的地方，称之为跨域
JSONP、CROS、代理
2.1:工作的时候 src 目录下的 API 文件夹，一般关于 axios 二次封装的文件
2.2 进度条：nprogress 模块实现进度条功能
工作的时候，修改进度条的颜色，修改源码样式.bar 类名的

