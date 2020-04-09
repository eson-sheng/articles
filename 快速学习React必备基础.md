# 快速学习`React`必备基础

## 概述
本文将从`React`的特点、如何使用`React`、`JSX`语法，然后会对组件（`Component`）以及组件的属性（`props`）、状态（`state`）、生命周期等方面进行讲解。
- 对`React`有个全面的认识
- 熟悉`JSX`基本语法
- 了解组件结构
- 熟悉组件的生命周期
- 学会使用`props`
- 学会使用`state`
- 熟悉自定义组件

## `React`是什么？
`React`是`Facebook`推出的开源`JavaScript Library`，它是一个用于组建用户界面的`JavaScript`库，让你以更简单的方式来创建交互式用户界面，它的出现让许多革新性的`Web`观念开始流行起来，例如：`Virtual DOM`、`Component`、申明式渲染等。

### 申明式与命令式

```
命令式编程：命令“机器”如何去做事情（how），这样不管你想要的是什么（what），它都会按照你的命令实现。
申明式编程：告诉“机器”你想要的是什么（what），让机器想出如何去做（how）。
```
- 申明式渲染
```javascript
const name = 'Eson';
const showView = '<div> Hi, <h1>{name}</h1> </div>';
ReactDOM.render(
    showView,
    document.getElementById('root')
);
```
- 命令式渲染
```javascript
document.querySelector('h1').innerText = 'Eson';
```

特点：
- 1.当数据改变时，`React`将高效的更新和渲染需要更新的组件。申明式视图使你的代码更可预测，更容易调试。
- 2.构建封装管理自己的状态的组件，然后将它们组装成复杂的用户界面。由于组件逻辑是用`JavaScript`编写的，而不是模板，所以你可以放松的通过你的应用程序传递丰富的数据，并保持`DOM`状态。
- 3.一次学习随处可写，学习`React`，你不仅可以将它用于`Web`开发，也可以用于`ReactNative`来开发`Android`和`iOS`应用。

如图：（不是模板却比模板更加灵活）
![react组件模板](https://api.eson.site/oss/?path=blogUploads/2020/04/react组件.jpg)
通过不同的组件封装而成，组件化的开发模式，使得代码在更大程度上得到复用，而且组件之间对的组装很灵活。

## 如何使用？
构建一个新的`React`单页应用，可以通过`create-react-app`脚手架工具来完成。
```shell
npm install -g create-react-app
create-react-app my-app
cd my-app
npm start
```
如`package.json`安利：
```json
"dependencies": {
    "react": "^16.11.0", // 核心库
    "react-dom": "^16.6.3", // 提供与DOM相关的功能
    "react-scripts": "2.1.1", // create-react-app 的核心包，一些脚本和工具的默认配置都集成在这里面
},
```

## `ReactDOM.render`
> ReactDOM.render(element, container[, callback])

渲染一个`React`元素到由`container`提供的`DOM`中，并且返回组件的一个引用（`reference`）或者对于 无状态组件 返回`null`。

## JSX
`JSX`是一个看起来很像`XML`的`JavaScript`语法扩展。每一个`XML`标签都会被`JSX`转换工具转换成纯`JavaScript`代码，使用`JSX`,组件的结构和组件之间的关系看上去更加清晰。`JSX`并不是`React`必须使用的，但`React`官方建议我们使用`JSX`,因为它能定义简洁且我们熟知的包含属性的树状结构语法。

> 使用`JSX`示例

```javascript
React.render(
    <div>
        <div>
            <div>content</div>
        </div>
    </div>,
    document.getElementById('example')
);
```

> 不使用`JSX`示例

```javascript
React.render(
    React.createElement(
        'div', null, React.createElement(
            'div', null, React.createElement('div', null, 'content')
        )
    ),
    document.getElementById('example')
);
```

## `createElement`
```javascript
React.createElement(type,[props],[...children])
```
根据给定的类型创建并返回新的`React element`。参数`type`既可以是一个`html`标签名称字符串（例如`div`或`span`），也可以是一个`React component`类型（一个类或一个函数）。
```javascript
React.createElement(Hello, {toWhat: 'World'}, 'hello'),
// 等价于 <Hello toWhat="World">hello</Hello>,
```








