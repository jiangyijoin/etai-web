
npm install找不到包 参见 [npm换源](#npm换源) 章节

***

# firebrand-admin

演示地址 <http://10.8.132.221:8025>

[快速开发指南](doc/getting-started.md)

## 特性

-   基于[react](https://github.com/facebook/react)，[ant-design](https://github.com/ant-design/ant-design)，[dva](https://github.com/dvajs/dva)，[Mock](https://github.com/nuysoft/Mock) 企业级后台管理系统最佳实践。
-   基于Antd UI 设计语言，提供后台管理系统常见使用场景。
-   基于[dva](https://github.com/dvajs/dva)动态加载 Model 和路由，按需加载。
-   使用[roadhog](https://github.com/sorrycc/roadhog)本地调试和构建，其中Mock功能实现脱离后端独立开发。
-   浅度响应式设计。

## 知识基础

-   ES6（重要）
    -   [30分钟掌握ES6/ES2015核心内容](https://segmentfault.com/a/1190000004365693)
    -   [ECMAScript 6 入门](http://es6.ruanyifeng.com/#docs/intro)
-   Dva（重要）
    -   [知识图](https://github.com/dvajs/dva-knowledgemap)
    -   [快速上手](https://github.com/dvajs/dva-docs/blob/master/v1/zh-cn/getting-started.md)
-   Antd (工具地址)
    -   [Component](https://ant.design/components/button-cn/)
-   React
    -   [React Hello World](https://doc.react-china.org/docs/hello-world.html)

## 环境搭建

### NodeJS环境搭建

-   [下载网址](https://nodejs.org/en/download/)
    根据格子环境下载安装对应版本

#### npm换源
```
npm config set registry http://10.8.132.161:8081/artifactory/api/npm/virtual161/

npm login
eastcom/eastcom
```

### git环境搭建

-   [git bash下载网址](https://git-scm.com/downloads)

### 项目部署

-   [firebrand-fire 项目GIT地址](http://10.8.132.164:8081/common/firebrand-admin/tree/master)

配置ssh公钥[详细文档](http://10.8.132.164:8081/help/ssh/README):

git bash 中输入 （注：git bash 不是 cmd）

```bash
ssh-keygen -t rsa -C "your.email@example.com" -b 4096
```

一直回车 cmd中执行

```bash
type %userprofile%\.ssh\id_rsa.pub | clip
```

（此时公钥已复制到剪贴板）
[gitlib-角色设置-sshkey](http://10.8.132.164:8081/profile/keys)中配置sshkey
![公钥粘贴位置](assets/公钥设置.png)

克隆项目文件:

```bash
git clone git@10.8.132.164:common/firebrand-admin.git
```

导出并切换到dev分支

```bash
git checkout -b framework origin/framework
```

进入目录安装依赖:

```bash
#开始前请确保没有安装roadhog、webpack到NPM全局目录
npm i 或者 yarn install
```

开发：

```bash
npm run build:dll #第一次npm run dev时需运行此命令，使开发时编译更快
npm run dev
打开 http://localhost:8000
```

## 工具安装

工具使用IDEA[下载网址](https://www.jetbrains.com/idea/download/)，下载Ultimate版，注册自己想办法

-   项目打开

-   nodejs插件安装  菜单[file-Settings]
    ![插件安装](assets/插件安装.gif)

-   快捷工具 -- [View -> ToolButtons]打开

## 规范

### 目录结构

```bash
├── /dist/           # 项目输出目录
├── /src/            # 项目源码目录
│ ├── /public/       # 公共文件，编译时copy至dist目录
│ ├── /components/   # UI组件及UI相关方法
│ ├── /routes/       # 路由组件
│ ├── /models/       # 数据模型
│ ├── /services/     # 数据接口
│ ├── /themes/       # 项目样式
│ │ ├── default.less # 全局样式
│ │ ├── index.less   # 样式入口
│ │ └── vars.less    # 全局样式变量
│ ├── /mock/         # 数据mock
│ ├── /utils/        # 工具函数
│ │ ├── config.js    # 项目常规配置
│ │ ├── index.js     # 常用工具方法
│ │ ├── request.js   # 异步请求函数
│ │ └── theme.js     # 项目需要在js中使用到样式变量
│ ├── route.js       # 路由配置
│ ├── index.js       # 入口文件
│ └── index.html     
├── package.json     # 项目信息
├── .eslintrc        # Eslint配置
└── .roadhogrc.js    # roadhog配置
```

### 命名及存储说明

-   components：**组件（方法）为单位** 以文件夹保存，文件夹名组件首字母大写（如`DataTable`），方法首字母小写（如`layer`）,文件夹内主文件与文件夹同名，多文件以`index.js`导出对象（如`./src/components/Layout`）。
-   routes：**页面为单位** 以文件夹保存，文件夹名首字母小写（特殊除外，如`UIElement`）,文件夹内主文件以`index.js`导出，多文件时可建立`components`文件夹，如果有子路由，依次按照路由层次建立文件夹(如`./src/routes/sysmanager/security/department/`）。
-   models:**页面为单位** 以文件保存，单一模块只绑定一个数据模型，模型名称为小写字母，如果有子模型，依次按照模型层次建立文件夹(如：`./src/routes/sysmanager/security/department/`)
-   service:**页面为单位** 以文件保存,依次按照路由层次建立文件夹(如`./src/service/sysmanager/security/department`）
-   mock:**接口模型为单位** 以文件保存，同一接口类型，放到同一文件下，mock按需求参照接口模型建造，mock前缀统一使用`/utils/config{MOCK_PFX}`,切换接口时统一在`/utils/config`中修改。
-   样式定义： `less`文件公共变量定义在`/themes/vars`下，公共样式定义定义在`/themes/default`，公共样式从优先级`/themes/index` > `/themes/default` > `/themes/vars` > `antd/lib/style/themes/default`

![接口类型](assets/接口类型.png)

## 数据流向

数据的改变发生通常是通过用户交互行为或者浏览器行为（如路由跳转等）触发的，当此类行为会改变数据的时候可以通过 dispatch 发起一个 action，如果是同步行为会直接通过 Reducers 改变 State ，如果是异步行为（副作用）会先触发 Effects 然后流向 Reducers 最终改变 State，所以在 dva 中，数据流向非常清晰简明，并且思路基本跟开源社区保持一致（也是来自于开源社区）。

![数据流向](assets/数据流向.png)

## Models

### State

`type State = any`

State 表示 Model 的状态数据，通常表现为一个 javascript 对象（当然它可以是任何值）；操作的时候每次都要当作不可变数据（immutable data）来对待，保证每次都是全新对象，没有引用关系，这样才能保证 State 的独立性，便于测试和追踪变化。

在 dva 中你可以通过 dva 的实例属性 `_store` 看到顶部的 state 数据，但是通常你很少会用到:

```javascript
const app = dva();
console.log(app._store); // 顶部的 state 数据
```

### Action

`type AsyncAction = any`

Action 是一个普通 javascript 对象，它是改变 State 的唯一途径。无论是从 UI 事件、网络回调，还是 WebSocket 等数据源所获得的数据，最终都会通过 dispatch 函数调用一个 action，从而改变对应的数据。action 必须带有 `type` 属性指明具体的行为，其它字段可以自定义，如果要发起一个 action 需要使用 `dispatch` 函数；需要注意的是 `dispatch` 是在组件 connect Models以后，通过 props 传入的。

    dispatch({
      type: 'add',
    });

### dispatch 函数

`type dispatch = (a: Action) => Action`

dispatching function 是一个用于触发 action 的函数，action 是改变 State 的唯一途径，但是它只描述了一个行为，而 dipatch 可以看作是触发这个行为的方式，而 Reducer 则是描述如何改变数据的。

在 dva 中，connect Model 的组件通过 props 可以访问到 dispatch，可以调用 Model 中的 Reducer 或者 Effects，常见的形式如：

```javascript
dispatch({
  type: 'user/add', // 如果在 model 外调用，需要添加 namespace
  payload: {}, // 需要传递的信息
});
```

### Reducer

`type Reducer<S, A> = (state: S, action: A) => S`

Reducer（也称为 reducing function）函数接受两个参数：之前已经累积运算的结果和当前要被累积的值，返回的是一个新的累积结果。该函数把一个集合归并成一个单值。

Reducer 的概念来自于是函数式编程，很多语言中都有 reduce API。如在 javascript 中：

```javascript
[{x:1},{y:2},{z:3}].reduce(function(prev, next){
    return Object.assign(prev, next);
})
//return {x:1, y:2, z:3}
```

在 dva 中，reducers 聚合积累的结果是当前 model 的 state 对象。通过 actions 中传入的值，与当前 reducers 中的值进行运算获得新的值（也就是新的 state）。需要注意的是 Reducer 必须是[纯函数](https://github.com/MostlyAdequate/mostly-adequate-guide/blob/master/ch3.md)，所以同样的输入必然得到同样的输出，它们不应该产生任何副作用。并且，每一次的计算都应该使用[immutable data](https://github.com/MostlyAdequate/mostly-adequate-guide/blob/master/ch3.md#reasonable)，这种特性简单理解就是每次操作都是返回一个全新的数据（独立，纯净），所以热重载和时间旅行这些功能才能够使用。

### Effect

Effect 被称为副作用，在我们的应用中，最常见的就是异步操作。它来自于函数编程的概念，之所以叫副作用是因为它使得我们的函数变得不纯，同样的输入不一定获得同样的输出。

dva 为了控制副作用的操作，底层引入了[redux-sagas](http://yelouafi.github.io/redux-saga/)做异步流程控制，由于采用了[generator的相关概念](http://www.ruanyifeng.com/blog/2015/04/generator.html)，所以将异步转成同步写法，从而将effects转为纯函数。至于为什么我们这么纠结于 **纯函数**，如果你想了解更多可以阅读[Mostly adequate guide to FP](https://github.com/MostlyAdequate/mostly-adequate-guide)，或者它的中文译本[JS函数式编程指南](https://www.gitbook.com/book/llh911001/mostly-adequate-guide-chinese/details)。

### Subscription

Subscriptions 是一种从 **源** 获取数据的方法，它来自于 elm。

Subscription 语义是订阅，用于订阅一个数据源，然后根据条件 dispatch 需要的 action。数据源可以是当前的时间、服务器的 websocket 连接、keyboard 输入、geolocation 变化、history 路由变化等等。

```javascript
import key from 'keymaster';
...
app.model({
  namespace: 'count',
  subscriptions: {
    keyEvent(dispatch) {
      key('⌘+up, ctrl+up', () => { dispatch({type:'add'}) });
    },
  }
});
```

## Router

这里的路由通常指的是前端路由，由于我们的应用现在通常是单页应用，所以需要前端代码来控制路由逻辑，通过浏览器提供的 [History API](http://mdn.beonex.com/en/DOM/window.history.html) 可以监听浏览器url的变化，从而控制路由相关操作。

dva 实例提供了 router 方法来控制路由，使用的是[react-router](https://github.com/reactjs/react-router)。

```javascript
import { Router, Route } from 'dva/router';
app.router(({history}) =>
  <Router history={history}>
    <Route path="/" component={HomePage} />
  </Router>
);
```

## Route Components

在[组件设计方法](https://github.com/dvajs/dva-docs/blob/master/v1/zh-cn/tutorial/04-%E7%BB%84%E4%BB%B6%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%B3%95.md)中，我们提到过 Container Components，在 dva 中我们通常将其约束为 Route Components，因为在 dva 中我们通常以页面维度来设计 Container Components。

所以在 dva 中，通常需要 connect Model的组件都是 Route Components，组织在`/routes/`目录下，而`/components/`目录下则是纯组件（Presentational Components）。

## 参考引申

-   [Dva数据流向](https://github.com/dvajs/dva/blob/master/docs/Concepts_zh-CN.md)
-   [redux docs](http://redux.js.org/docs/Glossary.html)
-   [redux docs 中文](http://cn.redux.js.org/index.html)
-   [Mostly adequate guide to FP](https://github.com/MostlyAdequate/mostly-adequate-guide)
-   [JS函数式编程指南](https://www.gitbook.com/book/llh911001/mostly-adequate-guide-chinese/details)
-   [choo docs](https://github.com/yoshuawuyts/choo)
-   [elm](http://elm-lang.org/blog/farewell-to-frp)
