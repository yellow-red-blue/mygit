# mygit
my git product
# 1.小程序的基本语法
## -页面基本介绍
  App() 必须在 app.js 中注册，且不能注册多个。
  编译后的代码包大小需小于 1MB，否则代码包将上传失败。
  每个页面需要手动在app.json中进行注册，否则不能访问。
  app.json中pages数组的第一项代表小程序的初始页面，小程序中新增/减少页面，都需要对 pages 数组进行修改。
  直接修改 this.data无效，无法改变页面的状态，还会造成数据不一致。
  单次设置的数据不能超过1024kB，请尽量避免一次设置过多的数据。
  不要尝试修改页面栈，会导致路由以及页面状态错误。
  tabBar只能配置最少2个、最多5个，tab 按数组的顺序排序。
  小程序页面只能同时打开 5 个，如果交互流程较长难以支持。
  同时只能存在 5 个url请求。
  没有cookie。
  没有开放加载web页面
  没有a标签链接，不可嵌套iframe
  没有window变量，但微信提供了wx全局方法集
  事件绑定和条件渲染类似Angular，全部写在WXML中
 ### 1.1 主体
  由app.js、app.json、app.wxss三个文件组成，放在根目录
  app.js 根目录的app.js很有用,因为在它内部注册的变量或方法，都是可以被所有页面获取到。可以监听并处理小程序的生命周期、声明全局变量。其余的.js文 件可以   通过var app = getApp() 获取其实例，调用其中定义的方法和变量，但不可以调用生命周期的方法
  app.json是小程序的全局配置
  pages 配置小程序的组成页面，第一个代表小程序的初始页面
  window  设置小程序的状态栏、标题栏、导航条、窗口背景颜色
  tabBar  配置小程序tab栏的样式和对应的页面
  app.wxss 是小程序的公共样式表，可以在其他.wxss文件中直接使用
  app.json
```
"pages": [ //设置页面的路径
  "pages/index/index", //不需要写index.wxml,index.js,index,wxss,框架会自动寻找并整合
  "pages/logs/logs"
],
"window": { //设置默认窗口的表现形式
  "navigationBarBackgroundColor": "#ffffff", //顶部导航栏背景色
  "navigationBarTextStyle": "black", //顶部导航文字的颜色 black/white
  "navigationBarTitleText": "微信接口功能演示", //顶部导航的显示文字
  "backgroundColor": "#eeeeee", //窗口的背景色
  "backgroundTextStyle": "light", //下拉背景字体、loading 图的样式，仅支持 dark/light
  "enablePullDownRefresh": "false"， //是否支持下拉刷新 ，不支持的话就直接不写！
  "disableScroll": true, //  设置true不能上下滚动，true/false，注意！只能在 page.json 中有效，无法在 app.json 中设置该项。
},
"tabBar": { //底部tab或者顶部tab的表现，是个数组，最少配置2个，最多5个
  "list": [{ //设置tab的属性，最少2个，最多5个
    "pagePath": "pages/index/index", //点击底部 tab 跳转的路径
    "text": "首页", //tab 按钮上的文字
    "iconPath": "../img/a.png", //tab图片的路径
    "selectedIconPath": "../img/a.png" //tab 在当前页，也就是选中状态的路径
  }, {
    "pagePath": "pages/logs/logs",
    "text": "日志"
  }],
  "color": "red", //tab 的字体颜色
  "selectedColor": "#673ab7", //当前页 tab 的颜色，也就是选中页的
  "backgroundColor": "#2196f3", //tab 的背景色
  "borderStyle": "white", //边框的颜色 black/white
  "position": "bottom" //tab处于窗口的位置 top/bottom
  },
"networkTimeout": { //默认都是 60000 秒一分钟
    "request": 10000, //请求网络超时时间 10000 秒
    "downloadFile": 10000， //链接服务器超时时间 10000 秒
      "uploadFile": "10000", //上传图片 10000 秒
    "downloadFile": "10000" //下载图片超时时间 10000 秒
  },
"debug": true //项目上线后，建议关闭此项，或者不写此项
```
### 1.2 pages
  pages文件夹里是小程序的各个页面，每个界面一般都由.wxml、.wxss、.js、.json四个文件组成，四个文件必须是相同的名字和路径

  .js 是页面的脚本代码，通过Page()函数注册页面。可以指定页面的初始数据、生命周期、事件处理等
  .wxml 是页面的布局文件，只能使用微信定义的组件
  .wxss 是样式表，需要注意
  尺寸单位：rpx 可以根据屏幕的宽带进行自适应
  样式导入：@import导入外联样式表，如：@import "test.wxss";
  定义在app.wxss中的全局样式，作用于每个页面。定义在page的.wxss文件只作用于对应的页面，会覆盖app.wxss中相同的选择器
  .json 是页面的配置文件，只能设置app.json中的window配置内容，会覆盖app.json中window的相同配置项，即使不配置任何东西也需要写{},否则会报错

## 2常用的api

