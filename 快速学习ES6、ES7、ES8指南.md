# 快速学习`ES6、ES7、ES8`基础指南

## 概述
`ECMAScript`版本 | 发布时间 | 新增特性 
----- | ----- | ----- 
`ES5` | 2009年11月 | 扩展了`Object`、`Array`、`Function`的功能
`ES6` | 2015年5月 | 类，模块化，箭头函数，函数参数默认值等
`ES7` | 2016年3月 | `includes`，指数操作符
`ES8` | 2017年6月 | `sync/await`，`Object.values()`，`Object.entries()`，`Stringpadding`等

# `ES6`的特性
安利几个常用的：
- 类
- 模块化
- 箭头函数
- 函数参数默认值
- 解构赋值
- 延展操作符
- 对象属性简写
- `Promise`
- `let const`

## 1.类 `class`
让`JavaScript`的面向对象编程变得更加简单和易于理解
```javascript
class Animal {
    // 构造函数，实例化的时候将会被调用，如果不指定，那么会有一个不带参数的默认构造函数
    constructor(name,color) {
        this.name = name;
        this.color = color;
    }
    // toString 原型对象上的属性
    toString() {
        console.log('name:' + this.name + ',color:' + this.color);
    }
}

var animal = new Animal('dog','white'); // 实例化Animal
animal.toString();

console.log(animal.hasOwnProperty('name')); // true
console.log(animal.hasOwnProperty('toString')); // false
console.log(animal.__proto__.hasOwnProperty('toString')); // true

class Cat extends Animal {
    constructor(action) {
        // 子类必须要在 constructor 中指定 super 函数，否则在新建实例的时候会报错。
        // 如果没有置顶 constructor。默认带 super 函数的 constructor 将会被添加。
        super('cat','white');
        this.action = action;
    }
    toString() {
        console.log(super.toString());
    }
}

var cat = new Cat('catch');
cat.toString();

// 实例 cat 是 Cat 和 Animal 的实例，和ES5完全一致
console.log(cat instanceof Cat); // true
console.log(cat instanceof Animal); // true
```

## 2.模块化`Module`
ES5不支持原生的模块化，在ES6中模块作为重要的组成部分被添加进来。模块的功能主要有`export`和`import`组成。每一个模块都有自己单独的作用域，模块之间的相互调用关系是通过`export`来规定模块对外暴露的接口，通过`import`来引用它模块提供的接口。同时还为模块创造了命名空间，防止函数的命名冲突。

### 导出`exprot`
ES6允许在一个模块中使用`export`来导出多个变量或者函数。
**导出变量**
```javascript
// test.js
export var name = 'Rainbow'
```
> ES6不仅支持变量的导出，也支持常量导出。`export const sqrt = Math.sqrt` // 导出常量

ES6将一个文件视为一个模块，上面的模块通过`exprot`向外输出了一个变量。一个模块也可以同时往外面输出多个变量。
```javascript
// test.js
var name = 'Rainbow';
var age = '22';
export {name, age};
```
**导出函数**
```javascript
// myModule.js
export function myModule(someArg) {
    return someArg;
}
```

### 导入`import`
定义好模块的输出以后就可以在另外一个模块通过`import`引用。
```javascript
import {myModule} from 'myModule'; // main.js
import {name, age} from 'test'; //test.js
```
> 关于`import`语句可以同时导入默认函数和其它变量。`import defaultMethod, {otherMethod} from 'xxx.js';`

## 3.箭头`Arrow`函数
这是ES6特性之一。`=>`不只是关键字`function`的简写，箭头函数与包围它的代码共享同一个`this`。

### 箭头函数的结构
```javascript
// 箭头函数的安利
()=>1
v=>v+1
()=>{
    alert("foo");
}
e=>{
    if(e == 0){
        return 0;
    }
    return 1000/e;
}
```

### 卸载监听器时的注意
> 错误的做法

```javascript
class PauseMenu extends React.Component{
    componentWillMount(){
        AppStateIOS.addEventListener('change', this.onAppPaused.bind(this));
    }
    componentWillUnmount(){
        AppstateIOS.removeEventListener('change', this.onAppPaused.bind(this));
    }
    onAppPaused(event){

    }
}
```

> 正确的做法

```javascript
class PauseMenu extends React.Component{
    constructor(props){
        super(props);
        this._onAppPaused = this.onAppPaused.bind(this);
    }
    componentWillMount(){
        AppStateIOS.addEventListener('change', this._onAppPaused);
    }
    componentWillUnmount(){
        AppstateIOS.removeEventListener('change', this._onAppPaused);
    }
    onAppPaused(event){

    }
}
```
除上述的做法外，还可以这样做：
```javascript
class PauseMenu extends React.Component{
    componentWillMount(){
        AppStateIOS.addEventListener('change', this.onAppPaused.bind(this));
    }
    componentWillUnmount(){
        AppstateIOS.removeEventListener('change', this.onAppPaused.bind(this));
    }
    onAppPaused = (event) => {
        // 把函数直接作为一个 arraw function 的属性来定义，初始化的时候就绑定好了this指针。
    }
}
```
> 注意：不论是`bind`还是箭头函数，每次被执行都返回的是一个新的函数引用，因此如果还需要函数的引用做其它事情，那么就要保存这个引用。

## 4.函数参数默认值
ES6支持在定义函数的时候为其设置默认值：
```javascript
function foo(height = 50, color = 'pink')
{
    // ...
}
```
> 不是用默认值

```javascript
function foo(height, color)
{
    var height = height || 50;
    var color = color || 'pink';
    // ...
}
```
这样一般没问题，但是`参数的布尔值为false`时，就会有问题了！例如：
```javascript
foo(0,"");
```
因为`0的布尔值为false`，这样height的取值就是50了，同理color取值就是pink了。

## 5.模板字符串
ES6支持模板字符串，使得字符串更加简洁直观。
> 不使用模板字符串

```javascript
var name = 'Your name is ' + first + ' ' + last + '.';
```

> 使用模板字符串

```javascript
var name = 'Your name is ${first} ${last}.';
```

## 6.解构赋值
解构赋值语法是`JavaScript`的一种表达式，可以方便的从数组或者对象中快速提取值赋给定义的变量。

### 获取数组中的值
从数组中获取值并赋值到变量中，变量的顺序与数组中对象顺序对应。
```javascript
var foo = ["one", "two", "three" ,"four"];

var [one,two,three] = foo;

console.log(one); // "one"
console.log(two); // "two"
console.log(three); // "three"

// 如果要忽略某些值，可以按照下面的写法获取值
var [first, , , last] = foo;
console.log(first); // "one"
console.log(last); // "four"

// 也可以这样编写
var a, b; //先申明变量
[a, b] = [1,2];
console.log(a); // 1
console.log(b); // 2
```

如果没有从数组中获取到值，可以为变量设置一个默认值。
```javascript
var a, b;
[a=5, b=7] = [1];
console.log(a); // 1
console.log(b); // 7
```

通过解构赋值可以方便的交换两个变量的值。
```javascript
var a=1;
var b=3;

[a, b] = [b, a];
console.log(a); // 3
console.log(b); // 1
```

### 获取对象中的值
```javascript
const student = {
    name:'Ming',
    age:'18',
    city:'Shanghai'
};

const {name,age,city} = student;
console.log(name); // "Ming"
console.log(age); // "18"
console.log(city); // "Shanghai"
```

## 7.延展操作符（Spread operator）
延展操作符`...`可以在函数调用数组构造时，将数组表达式或者`string`在语法层面展开；还可以在构造对象时，将对象表达式按`key-value`的方式展开。

### 语法
> 函数调用：

```javascript
myFunction(...iterableObj);
```

> 数组构造或字符串：

```javascript
[...iterableObj, '4', ...'hello', 6];
```

> 构造对象时，进行克隆或者属性拷贝（ECMAScript2018规范新特性）：

```javascript
let objClone = { ...obj };
```

### 应用场景
> 在函数调用时使用延展操作符

```javascript
function sum(x, y, z){
    return x + y + z;
}
const numbers = [1, 2, 3];

// 不使用延展操作符
console.log(sum.apply(null, numbers)); // 6

// 使用延展操作符
console.log(sum(...numbers)); // 6
```

> 构造数组

没有展开语法的时候，只能组合使用 `push`，`splice`，`concat`等方法，来将已有数组元素变成新数组的一部分。有了展开语法，构造新数组会变得更简单、更优雅：

```javascript
const stuendts = ['Jine','Tom'];
const persons = ['Tony', ... stuendts,'Aaron','Anna'];
console.log(persions)// ["Tony", "Jine", "Tom", "Aaron" ,"Anna"];
```
和参数列表的展开类似，`...`在构造数组时，可以在任意位置多次使用。

> 数组拷贝

```javascript
var arr = [1, 2, 3];
var arr2 = [...arr]; // 等同于 arr.slice()
arr2.push(4);
console.log(arr2); // [1, 2, 3, 4]
```

展开语法和`Object.assign()`行为一致，执行的都是浅拷贝（只遍历一层）。

> 链接多个数组

```javascript
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
var arr3 = [...arr1, ...arr2]; // 将 arr2 中所有元素附加到 arr1 后面并返回
// 等同于
var arr4 = arr1.concat(arr2);
```

### 在ECMAScript 2018中延展操作符增加了对对象的支持：
```javascript
var obj1 = { foo: 'bar', x:42 };
var obj2 = { foo: 'baz', y:13 };

var cloneObj = { ...obj1 };
// 克隆后的对象： { foo: "bar", x:42 }

var mergedObj = { ...obj1, ...obj2 };
// 合并后的对象：{ foo: "baz", x: 42 y: 13 }
```

### 在`React`中的应用
通常我们在封装一个组件时，会对外公开一些`props`用于实现功能。大部分情况下在外部使用都应显示的传递`props`。但是当传递大量的`props`时，会非常繁琐，这时我们可以使用 `...`(延展操作符，用于取出参数对象的所有可遍历属性)来进行传递。

### 一般情况下应该的安利：
```javascript
<CustomComponent name ='Jine' age = {21} />
```
> 使用`...`,等同于上面的写法

```javascript
const params = {
    name: "Jine",
    age: 21
}
<CustomComponent {...params} />
```
> 配合结构赋值避免传入一些不需要的参数

```javascript
var params = {
    name: '123',
    title: '456',
    type: 'aaa',
}
var { type, ...other } = params;

<CustomComponent type='normal' number={2} {...other} />
// 等同于
<CustomComponent type='normal' number={2} name='123' title='456' />
```

## 8.对象属性简写
在ES6中允许我们在设置一个对象的属性的时候不指定属性名。
> 不使用ES6

```javascript
const name = 'Ming' , age = '18' , city = 'Shanghai';

const student = {
    name:name,
    age:age,
    city:city
}
console.log(student); // {name: "Ming", age: "18", city: "Shanghai"}
```
对象中必须包含属性和值，显得非常沉余。
> 使用ES6

```javascript
const name = "Ming",age="18",city="Shanghai";

const student = {
    name,
    age,
    city
};
console.log(student); // {name: "Ming", age: "18", city: "Shanghai"}
```
对象中直接写变量，非常简洁。

## 9.`Promise`
`Promise` 是异步编程的一种解决方案，比传统的解决方案`callback`更加优雅。它最早是由社区提出和实现的，`ES6`将其写进了语言标准，统一了用法，原生提供了`Promise`对象。
> 不使用ES6

嵌套两个`setTimeout`回调函数：
```javascript
setTimeout(function(){
    console.log('hello'); // 1秒后输出"hello"
    setTimeout(function(){
        console.log('hi'); // 2秒后输出"hi"
    }, 1000);
}, 1000);
```

> 使用ES6

```javascript
var waitSecond = new Promise(function(resolve, reject){
    setTimeout(resolve, 1000);
});

waitSecond.then(function(){
    console.log("hello"); // 1秒后输出"hello"
    return waitSecond;
}).then(function(){
    console.log('hi'); // 2秒后输出"hi"
});
```
上面的代码使用两个`then`来进行异步编程串行化，避免了回调地狱。

## 10.支持`let`与`const`
在之前JS是没有块级作用域的，const与let填补了这方面的空白，const与let都是块级作用域。
> 使用`var`定义的变量为函数级作用域：

```javascript
{
    var a = 10;
}
console.log(a); // 输出10
```
> 使用`let`与`const`定义的变量为块级作用域：

```javascript
{
    let a = 10;
}
console.log(a); // Uncaught ReferenceError: a is not defined
```
# `ES7`的新特性
在ES6之后，ES的发布频率更加频繁，基本每年一次，所以自ES6之后，每个版本的特性的数量就比较少。
- `includes()`
- 指数操作符

## 1.`Array.prototype.includes()`
`includes()`函数用来判断一个数组是否包含一个指定的值，如果包含则返回`true`,否则犯规`false`。
`includes()`函数与`indexOf`函数很相似，下面两个表达式是等价的：
```javascript
arrincludes(x);
arr.indexOf(x) >= 0;
```
接下来看判断数字中是否包含某个元素：
> 在ES7之前的做法

使用`indexOf()`验证数组中是否存在某个元素，这时需要根据返回值是否为`-1`来判断：
```javascript
let arr = ['react', 'angular', 'vue'];

if (arr.indexOf('react') !== -1 ) {
    console.log('react 存在');
}
```
> 使用ES7的`includes()`

使用`includes()`验证数组中是否存在某个元素，这样更加直观简单：
```javascript
let arr = ['react', 'angular', 'vue'];

if (arr.includes('react')) {
    console.log('react 存在');
}
```

## 2.指数操作符
在ES7中引入了指数运算符`**`，`**`具有与`Math.pow(..)`等效的计算结果。
> 不使用指数操作符

使用自定义的递归函数`calculateExponent`或者`Math.pow()`进行指数运算：
```javascript
function calculateExponent(base, exponent){
    if (exponent === 1) {
        return base;
    } else {
        return base * calculateExponent(base, exponent-1);
    }
}
```
> 使用指数操作符

使用指数运算符`**`，就像`+`、`-`等操作符一样：
```javascript
console.log(2**10); // 输出1024
```

# ES8的特性
- `async/await`
- `Object.values()`
- `Object.entries()`
- `String padding`
- 函数参数列表结尾允许逗号
- `Object.getOwnPropertyDescriptors()`

## 1.`async/await`
在ES8中加入了对`async/await`的支持，也就是所说的`异步函数`，这是一个很实用的功能。`async/await`将我们从头痛的回调地狱中解脱出来了，使整个代码看起来很简洁。
> 使用`async/await`与不使用`async/await`的差别：

```javascript
login(userName){
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            resolve('1001');
        }, 600);
    });
}

getData(userID){
    return new Promise((resolve, reject) => {
        setTimeout(()=>{
            if (userID === '1001') {
                resolve('SUCCESS');
            } else {
                reject('FAIL');
            }
        },600);
    });
}

// 不使用async/await ES7
doLogin(userName){
    this.login(userName).then(this.getData).then(result => {
        console.log(result);
    });
}

// 使用async/await ES8
async doLogin2(userName) {
    const userID = await this.login(userName);
    const result = await this.getData(userID);
}

this.doLogin(1);// SUCCESS
this.doLogin2(1);// SUCCESS
```

### `async/await`的几种应用场景
> 获取异步函数返回值

异步函数本身返回一个`Promise`，所以可以通过`then`来获取异步函数的返回值。
```javascript
async function charCountAdd(data1,data2){
    const d1 = await charCount(data1);
    const d2 = await charCount(data2);
    return d1+d2;
}
charCountAdd('Hello', 'Hi').then(console.log); //通过then获取异步函数的返回值
function charCount(data){
    return new Promise((resolve, reject) => {
        setTimeout(()=>{
            resolve(data.length);
        }, 1000);
    });
}
```
> `async/await`在并发场景中的应用

对于上诉的例子，我们调用`await`两次，每次都是等待1秒一共是2秒，效率比较低，而且两次`await`的调用并没有依赖关系，那能不能让其并发执行呢？答案是肯定的，接下来通过`Promise.all`来实现`await`的并发调用。

```javascript
async function charCountAdd(data1, data2){
    const [d1,d2] = await Promise.all([charCount(data1),charCount(data2)]);
    return d1+d2;
}
charCountAdd('Hello','Hi').then(console.log);
function charCount(data) {
    return new Promise( (resolve, reject) => {
        setTimeout( () => {
            resolve(data.length);
        }, 1000);
    });
}
```
通过上述代码实现了两次`charCount`的并发调用，`Promise.all`接受的是一个数组，它可以将数组中的`Promise`对象并发执行。

### `async/await`的几种错误处理

第一种：捕捉整个`async/await`函数的错误
```javascript
async function charCountAdd(data1, data2){
    const d1 = await charCount(data1);
    const d2 = await charCount(data2);
    return d1+d2;
}
charCountAdd('Hello','Hi').then(console.log).catch(console.log);//捕捉整个`async/await`函数的错误
```
这种方式可以捕捉整个`charCountAdd`运行过程中出现的错误，错误可能是由`charCountAdd`本身产生的，也可能是由对`data1`的计算中或`data2`的计算中产生的。

第二种：捕捉单个的`await`表达式的错误
```javascript
async function charCountAdd(data1, data2) {
    const d1 = await charCount(data1).catch(e => console.log('d1 is null'));
    const d2 = await charCount(data2).catch(e => console.log('d2 is null'));
    return d1+d2;
}
charCountAdd('Hello','Hi').then(console.log);
```
通过这种方式可以捕捉每一个`await`表达式错误。如果既要捕捉每个`await`表达式错误，又要捕捉整个`charCountAdd`函数的错误，可以在调用`charCountAdd`的时候加个`catch`进行捕捉。
```javascript
charCountAdd('Hello','Hi').then(console.log).catch(console.log);// 捕捉整个async/await函数错误
```

第三种：同时捕捉多个`await`表达式的错误
```javascript
async function charCountAdd(data1, data2) {
    let d1,d2;
    try {
        d1 = await charCount(data1);
        d2 = await charCount(data2);
    } catch (e) {
        console.log(e);
    }
    return d1+d2;
}
charCountAdd('Hello','Hi').then(console.log);
function charCount(data) {
    return new Promise( (resolve, reject) => {
        setTimeout( () => {
            resolve(data.length);
        }, 1000); 
    });
}
```

## 2.`Object.values()`
`Object.values()`是一个与`Object.keys()`类似的新函数，但返回的是`Object`自身属性的所有值，不包括继承的值。
假设我们要遍历如下对象`obj`的所有值：
```javascript
const obj = {a:1, b:2, c:3};
```
> 不使用`Object.values()`:`ES7`

```javascript
const val = Object.keys(obj).map(key => obj[key]);
console.log(val);// [1,2,3]
```
> 使用`Object.values()`:`ES8`

```javascript
const values = Object.values(obj);
console.log(values); // [1,2,3]
```
从上述代码中可以看出`Object.values()`为我们省去了遍历`key`，并根据这些`key`获取`value`的步骤。

## 3.`Object.entries`
`Object.entries()`函数返回一个给定对象自身可枚举属性的键值对的数组。
接下来我们来遍历上文中的`obj`对象的所有属性的`key`和`value`:
> 不使用`Object.entries()`:`ES7`

```javascript
Object.keys(obj).forEach(key => {
    console.log('key:' + key + ' value:' + obj[key]);
});
// key:a value:1
// key:b value:2
// key:c value:3
```
> 使用`Object.entries()`:`ES8`

```javascript
for(let [key,value] of Object.entries(obj)) {
    console.log(`key: ${key} value:${value}`);
}
// key:a value:1
// key:b value:2
// key:c value:3
```

## 4.`String padding`
在`ES8`中`String`新增了两个实例函数`String.prototype.padStart`和`String.prototype.padEnd`，允许将空字符串或其他字符串添加到原始字符串的开头或结尾。
> `String.padStart(targetLength,[padString])`

- `targetLength`:当前字符串需要填充到的目标长度。如果这个数值小于当前字符串的长度，则返回当前字符串本身。
- `padString`:（可选）填充字符串。如果字符串太长，使填充后的字符串长度超过了目标长度，则只保留最左侧的部分，其他部分会被截断，此参数的缺省值为“ ”。
```javascript
console.log('0.0'.padStart(4,'10')); //10.0
console.log('0.0'.padStart(20)); //                  0.0
```

> `String.padEnd(targetLength,[padString])`

- `targetLength`:当前字符串需要填充到的目标长度。如果这个数值小于当前字符串的长度，则返回当前字符串本身。
- `padString`:（可选）填充字符串。如果字符串太长，使填充后的字符串长度超过了目标长度，则只保留最左侧的部分，其他部分会被截断，此参数的缺省值为“ ”。
```javascript
console.log('0.0'.padEnd(4,'0')); //0.00
console.log('0.0'.padEnd(10,'0')); //0.00000000
```

## 5.函数参数列表结尾允许逗号
一个小更新而已，不用多说了。只是方便应用而已。
```javascript
var f = function(a, b, c,){
    // tudo
}
```

## 6.`Object.getOwnPropertyDescriptors()`
`Object.getOwnPropertyDescriptors()`函数用来获取一个对象的所有自身属性的描述符，如果没有任何属性，则返回空对象。
> 函数原型：

```javascript
Object.getOwnPropertyDescriptors(obj)
```
返回`obj`对象的所有自身属性的描述符，如果没有任何属性，则返回空对象。
```javascript
const obj = {
    name: 'eson',
    get age() {
        return '18';
    }
};
Object.getOwnPropertyDescriptors(obj);
```

# 总结
技术更替的车轮一直在前进中，`JavaScript`的规范和标准也在不断的制定和完善。发现`ECMAScript`新版的很多特效已经是`Typescript`，浏览器或其他`polyfills`的一部分，例如`ES8`的`async/await`来说，它是2017年6月被纳入`ECMAScript`的，但是2016年的时候就已经开始使用这个特性了，这些特性通常由`ECMAScript`议员提交，然后会出现在未来的某个`ECMAScript`版本中。


------------

[hermit auto="1" loop="0" unexpand="1" fullheight="0"]remote#:35[/hermit]
