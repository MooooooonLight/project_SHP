Swiper 使用步骤：
第一步：引入依赖包【swiper.js|swiper.css】
第二步:静态页面中结构必须完整【container、wrap、slider】，类名不能瞎写
第三步:初始化 swiper 实例

1:swiper 在 Vue 项目中使用 （开发 ListContainer 组件【首页 banner 图片】）
如何卸载插件：可以不用删除 node_modules 文件夹，可以使用 npm uninstall xxxx 进行卸载
1.1swiper 安装到项目当中

1.2 在相应的组件引入 swiper.js|swiper.css

但是需要注意，home 模块很多组件都使用到 swiper.css,没必要在每一个组件内部都引入样式一次，
只需要在入口文件引入一次即可。

1.3:初始化 swiper 实例在哪里书写?
初始化 swiper 实例之前，页面中的节点（结构）务必要有，
对于 Vue 一个组件而言 mounted-->组件挂载完毕

1.4 动态效果为什么没有出来？
Swiper 需要获取到轮播图的节点 DOM，才能给 swiper 轮播添加动态效果，因为没有获取到节点。

1.5 第一种解决方案，延迟器（不是完美的解决方案）
created 里面：created 执行与 mounted 执行，时间差可能 2ms
updated 里面：如果组件有很多响应式（data），只要有一个属性值发生变化 updated 还会再次执行，再次初始化实例。

总结：第一种解决方案可以通过延迟器（异步）去解决问题，
但是这种解决方案存在风险（无法确定用户请求到底需要多长时间），因此没办法确定延迟器时间。

2:Swiper 在 Vue 项目中使用完美解决方案
第一种解决方案问题出现在哪里：v-for,在遍历来自于 Vuex（数据:通过 ajax 向服务器发请求，存在异步）

watch:监听属性，watch 可以检测到属性值的变化，当属性值发生变化的时候，可以触发一次。

Vuex 当中的仓库数据 bannerList（组件在使用）：
bannerList 仓库数据有没有发生过变化？
一定是有的：bannerList 初始值空数组，当服务器的数据返回以后，它的 bannerList 存储的属性值会发生变化【变为服务器返回的数据】
组件实例在使用仓库中的 bannerList，组件的这个属性 bannerList 一定是发生过变化，watch 可以监听到。

组件实例的一个方法:$nextTick
this.$nextTick(()=>{

})
nextTick 官网解释:
在下次 DOM 更新, 循环结束之后,执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM。
注意：组件实例的$nextTick 方法，在工作当中经常使用，经常结合第三方插件使用，获取更新后的 DOM 节点

总结:
1:Swiper 插件工作中很常用（API、基本使用方法）
2:组件实例的$nextTick 方法。
在下次 DOM 更新, 循环结束之后,执行延迟回调。在 修改数据之后 立即使用这个方法，获取更新后的 DOM

3)开发 Floor 组件
开发 Floor 组件：Floor 重复使用两次

3.1:Floor 组件获取 mock 数据，派发 action 应该是在父组件的组件挂载完毕生命周期函数中书写，因为父组
件需要通知 Vuex 发请求，父组件获取到 mock 数据，通过 v-for 遍历 生成多个 floor 组件，因此达到复用作用。

3.2:父组件派发 action，通知 Vuex 发请求，Home 父组件获取仓库的数据，通过 v-for 遍历出多个 Floor 组件

3.3v-for|v-show|v-if|这些指令可以在自定义标签（组件）的身上使用

3.4 组件间通信面试必问
props:父子
插槽:父子
自定义事件:子父
全局事件总线$bus:万能
pubsub:万能
Vuex:万能
$ref:父子通信
3.5 为什么在 Floor 组件的 mounted 中初始化 SWiper 实例轮播图可以使用.
因为父组件的 mounted 发请求获取 Floor 组件数据，当父组件的 mounted 执行的时候。
Floor 组件结构可能没有完整，但是服务器的数据回来以后 Floor 组件结构就一定是完成的了
，因此 v-for 在遍历来自于服务器的数据，如果服务器的数据有了，Floor 结构一定的完整的。
否则，都看不见 Floor 组件

4)carousel 全局组件
如果项目当中出现类似的功能，且重复利用，封装为全局组件

为了封装全局的轮播图组件:让 Floor 与 listContainer 组件中的代码一样，如果一样完全可以独立出来
封装为一个全局组件。
