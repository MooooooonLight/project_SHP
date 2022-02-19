项目十三天:
发现:基础知识点-->回首复习
分页
购物车
登录、注册

1)交易业务
前面课程当中可能自己已经注册了一个账号【18666666661】，今天在做支付的时候，统一使用
账号:13700000000
密码:111111

1.1 获取用户地址信息、获取用户购物车清单信息
//用户地址信息
/api/user/userAddress/auth/findUserAddressList
//商品清单接口
/api/order/auth/trade

1.2Vuex 的 action 发请求，但是从今天开始，咱们要练习不用 Vuex 改如何开发？
请求配置,类似$bus 使用
不要再声明周期函数中使用 async

2)展示商品清单数据

3)提交订单业务

当用户点击提交订单按钮的时候，需要发请求的
提交订单的请求地址:/api/order/auth/submitOrder?tradeNo={tradeNo}

前台：需要告诉服务器：谁买的、买的啥、买几个、 支付多少钱、留言信息...
后台：订单号，这笔交易的一个标识符【支付的】

axios({url:'xxx',methods:'post',data:{a:1}})

3.1 微信支付、支付宝支付等等
交易编码（服务器：字符串 hash）
收件人名字
收件人手机号
收件的地址
买家留言信息
支付产品

4)获取支付信息进行展示

5)element-ui 官方 UI 组件库（插件）？

react 框架:
UI 组件库 antd【蚂蚁金服旗下 PC 端 UI 组件库】
antd-mobile【蚂蚁金服旗下的移动端 UI 组件库】

Vue 框架:
element-UI【饿了吗旗下的 UI 组件库，官方承认的 PC 组件库插件】
vant【Vue 官方提供移动端 UI 组件库】

官网地址:https://element.eleme.cn/#/zh-CN
官网地址：https://youzan.github.io/vant/#/zh-CN/

第一步：项目中安装 element-ui 组件库 [2.15.6 版本：Vue2]

第二步：在入口文件引入 elementUI 组件库
第一种：全部引入【不采用：因为项目中只是用到一个组件，没必要全都引入进来】
第二种：按需引入【按照开发需求引入相应的组件，并非全部组件引入】

第三步：按需引入，安装相应的插件
cnpm install babel-plugin-component -D
文档中说的.babelrc 文件，即为 babel.config.js 文件
修改完 babel.config.js 配置文件以后，项目重启

第四部：按照需求引入相应的组件即可

Vue.component();
Vue.prototype.$xxx = xxx;

6)支付业务【微信支付】
this.$alert('<strong>这是 <i>HTML</i> 片段</strong>', 'HTML 片段', {dangerouslyUseHTMLString: true});
6.1 今晚稍微把 elementUI 的组件都稍微看看。
6.2 使用 messageBox 显示弹框
6.3 展示二维码----qrcode 插件
通过 qrCode.toDataUrl 方法，将字符串转换为加密的在线二维码链接，通过图片进行展示。
moment.js
swiper.js
nprogress.js
qrcode.js

GET|POST：短轮询，请求发一次，服务器响应一次，完事。

第一种做法:前端开启定时器，一直找服务器要用户支付信息【定时器】

第二种做法:项目务必要上线 + 和后台紧密配合
当用户支付成功以后，需要后台重定向到项目某一个路由中，将支付情况通过 URL 参数形式传给前端，
前端获取到服务器返回的参数，就可以判断了。
