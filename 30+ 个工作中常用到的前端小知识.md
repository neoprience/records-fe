

1. JS为什么单线程

一个简单的原因就是，js在设计之初只是进行一些简单的表单校验，这完全不需要多线程，单线程完全可以胜任这项工作。即便后来前端发展迅速，承载的能力越来越多，也没有发展到非多线程不可的程度。

而且还有一个主要的原因，设想一下，如果js是多线程的，在运行时多个线程同时对DOM元素进行操作，那具体以哪个线程为主就是个问题了，线程的调度问题是一个比较复杂的问题。

HTML5新的标准中允许使用new Worker的方式来开启一个新的线程，去运行一段单独的js文件脚本，但是在这个新线程中严格的要求了可以使用的功能，比如说他只能使用ECMAScript, 不能访问DOM和BOM。这也就限制死了多个线程同时操作DOM元素的可能。

2.使用css写出一个三角形角标
元素宽高设置为0，通过border属性来设置，让其它三个方向的border颜色为透明或者和背景色保持一致，剩余一条border的颜色设置为需要的颜色。

div {
    width: 0;
    height: 0;
    border: 5px solid #transparent;
    border-top-color: red;
}
3.水平垂直居中
我一般只使用两种方式定位或者flex，我觉得够用了。

div {
    width: 100px;
    height: 100px;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    margin: auto;
}
父级控制子集居中

.parent {
    display: flex;
    justify-content: center;
    align-items: center;
}
4. css一行文本超出...
overflow: hidden;
text-overflow:ellipsis;
white-space: nowrap;
5.多行文本超出显示...
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 3;
overflow: hidden;
6.IOS手机容器滚动条滑动不流畅
overflow: auto;
-webkit-overflow-scrolling: touch;
7.修改滚动条样式
隐藏div元素的滚动条

div::-webkit-scrollbar {
    display: none;
}
div::-webkit-scrollbar 滚动条整体部分

div::-webkit-scrollbar-thumb 滚动条里面的小方块，能向上向下移动（或往左往右移动，取决于是垂直滚动条还是水平滚动条）

div::-webkit-scrollbar-track 滚动条的轨道

div::-webkit-scrollbar-button 滚动条的轨道的两端按钮，允许通过点击微调小方块的位置。

div::-webkit-scrollbar-track-piece 内层轨道，滚动条中间部分

div::-webkit-scrollbar-corner 边角，即两个滚动条的交汇处

div::-webkit-resizer 两个滚动条的交汇处上用于通过拖动调整元素大小的小控件

注意此方案有兼容性问题，一般需要隐藏滚动条时我都是用一个色块通过定位盖上去，或者将子级元素调大，父级元素使用overflow-hidden截掉滚动条部分。暴力且直接。

8.解决ios audio无法自动播放、循环播放的问题
ios手机在使用audio或者video播放的时候，个别机型无法实现自动播放，可使用下面的代码hack。

// 解决ios audio无法自动播放、循环播放的问题
var music = document.getElementById('video');
var state = 0;

document.addEventListener('touchstart', function(){
    if(state==0){
        music.play();
        state=1;
    }
}, false);

document.addEventListener("WeixinJSBridgeReady", function () {
    music.play();
}, false);

//循环播放
music.onended = function () {
    music.load();
    music.play();
}
9.隐藏页面元素
display-none: 元素不会占用空间，在页面中不显示，子元素也不会显示。

opacity-0: 元素透明度将为0，但元素仍然存在，绑定的事件仍旧有效仍可触发执行。

visibility-hidden：元素隐藏，但元素仍旧存在，占用空间，页面中无法触发该元素的事件。

10.前端工程化
一提到前端工程化很多人想到的都是webpack，这是不对的，webpack仅仅是前端工程化中的一环。在整个工程化过程中他帮我们解决了绝大多数的问题，但并没有解决所有问题。

前端工程化是通过工具提升效率，降低成本的一种手段。

近些年被广泛的关注和探讨，究其原因主要是因为现代化前端应用功能要求不断提高，业务逻辑日益复杂，作为当下互联网时代唯一不可或缺的技术，前端可以说是占据了整个开发行业的半壁江山。从传统的网站，到现在的H5,移动App,桌面应用，以及小程序。前端技术几乎是无所不能的全面覆盖。

在这些表象的背后呢，实际上是行业对开发人员的要求发生了天翻地覆的变化，以往前端写demo，套模板，调页面这种刀耕火种的方式已经完全不符合当下对开发效率的要求，前端工程化就是在这样一个背景下被提上台面，成为前端工程师必备的手段之一。

一般来说前端工程包含，项目初始化，项目开发，提交，构建，部署，测试，监控等流程。工程化就是以工程的角度来解决这些问题。比如项目初始化我们一般使用npm init, 创建页面模板使用plop，我们喜欢使用ES6+开发，但是需要通过babel编码成ES5，持续集成的时候我们使用git/ci cd，但是为了保持开发规范我们引入了ESLint，部署一般使用git/cd或者jenkins等等。

11.contenteditable
html中大部分标签都是不可以编辑的，但是添加了contenteditable属性之后，标签会变成可编辑状态。

<div contenteditable="true"></div>
不过通过这个属性把标签变为可编辑状态后只有input事件，没有change事件。也不能像表单一样通过maxlength控制最大长度。我也忘记我在什么情况下用到过了，后面想起来再补吧。

12.calc
这是一个css属性，我一般称之为css表达式。可以计算css的值。最有趣的是他可以计算不同单位的差值。很好用的一个功能，缺点是不容易阅读。接盘侠没办法一眼看出20px是啥。

div {
    width: calc(25% - 20px);
}
13.Date对象
获取当前时间毫秒值

// 方式一
Date.now(); // 1606381881650
// 方式二
new Date() - 0; // 1606381881650
// 方式三
new Date().getTime() // 1606381881650
创建Date对象的兼容性问题。

// window和安卓支持，ios和mac不支持
new Date('2020-11-26'); 
// window和安卓支持，ios和mac支持
new Date('2020/11/26');
14.Proxy和Object.defineProperty区别
Proxy的意思是代理，我一般叫他拦截器，可以拦截对象上的一个操作。用法如下，通过new的方式创建对象，第一个参数是被拦截的对象，第二个参数是对象操作的描述。实例化后返回一个新的对象，当我们对这个新的对象进行操作时就会调用我们描述中对应的方法。

new Proxy(target, {
    get(target, property) {

    },
    set(target, property) {

    },
    deleteProperty(target, property) {

    }
})
Proxy区别于Object.definedProperty。

Object.defineProperty只能监听到属性的读写，而Proxy除读写外还可以监听属性的删除，方法的调用等。

通常情况下我们想要监视数组的变化，基本要依靠重写数组方法的方式实现，这也是Vue的实现方式，而Proxy可以直接监视数组的变化。

const list = [1, 2, 3];
const listproxy = new Proxy(list, {
    set(target, property, value) {
        target[property] = value;
        return true; // 标识设置成功
    }
});

list.push(4);
Proxy是以非入侵的方式监管了对象的读写，而defineProperty需要按特定的方式定义对象的属性。

15.Reflect
他是ES2015新增的对象，纯静态对象也就是不能被实例画，只能通过静态方法的方式调用，和Math对象类似，只能类似Math.random()的方式调用。

Reflect内部封装了一系列对对象的底层操作，一共14个，其中1个被废弃，还剩下13个。

Reflect的静态方法和Proxy描述中的方法完全一致。也就是说Reflect成员方法就是Proxy处理对象的默认实现。

Proxy对象默认的方法就是调用了Reflect内部的处理逻辑，也就是如果我们调用get方法，那么在内部，Reflect就是将get原封不动的交给了Reflect，如下。

const proxy = new Proxy(obj, {
    get(target, property) {
        return Reflect.get(target, property);
    }
})
Reflect和Proxy没有绝对的关系，我们一般将他们两个放在一起讲是为了方便对二者的理解。

那为什么会有Reflect对象呢，其实他最大的用处就是提供了一套统一操作Object的API。

判断对象是否存在某一个属性，可以使用in操作符，但是不够优雅，还可以使用Reflect.has(obj, name); 删除一个属性可以使用delete，也可以使用Reflect.deleteProperty(obj, name); 获取所有属性名可以使用Object.keys, 也可以使用Reflect.ownKeys(obj); 我们更推荐使用Reflect的API来操作对象，因为他才是未来。

16.解析get参数
通过replace方法获取url中的参数键值对，可以快速解析get参数。

const q = {};
location.search.replace(/([^?&=]+)=([^&]+)/g,(_,k,v)=>q[k]=v);
console.log(q); 
17.解析连接url
可以通过创建a标签，给a标签赋值href属性的方式，获取到协议，pathname，origin等location对象上的属性。

// 创建a标签
const aEle = document.createElement('a');
// 给a标签赋值href路径
aEle.href = '/test.html';
// 访问aEle中的属性
aEle.protocol; // 获取协议
aEle.pathname; // 获取path
aEle.origin;
aEle.host;
aEle.search;
...
18.localStorage
localStorage是H5提供的永久存储空间，一般最大可存储5M数据，并且支持跨域隔离，他的出现极大提高了前端开发的可能性。localStorage的使用很多人都知道setItem，getItem,removeItem, 但他也可以直接以成员的方式操作。

// 存储
localStorage.name = 'yd';
// 获取
localStorage.name; // yd
// 删除
delete localStorage.name;
// 清除全部
localStorage.clear();

// 遍历
for (let i = 0; i < localStorage.length; i++) {
    const key = localStorage.key(i); // 获取本地存储的Key
    localStorage[key]; // 获取本地存储的value
}
localStorage满了的情况下仍继续存储并不会覆盖其他的值，而是直接报错(QuotaExceededError)，并且当前存储的值也会被清空。浏览器支持每个域名下存储5M数据。

19.sessionStorage
sessionStorage和localStorage的区别是，存在当前会话，很多人理解的是浏览器关闭，这是不对的，假设你在A页面存储了sessionStorage，新开选项卡将A页面的链接粘贴进去打开页面，sessionStorage也是不存在的。

所以sessionStorage存在的条件是页面间的跳转，A页面存储了sessionStorage，他要通过超链接或者location.href或者window.open来打开另一个同域页面才能访问sessionStorage。

这一点在混合开发嵌套H5的开发模式中尤为重要，如果以新开webview的方式打开页面，很可能sessionStorage就没有了。

20.会话cookie
cookie在设置的时候如果不设置过期时间，就表示是个会话cookie，以前我以为关闭浏览器会话cookie就消失了，然而...喜提bug一个。

在多数情况下windows系统或者安卓系统确实是这样的。但是在macOS系统或者ios系统中，关闭浏览器并不会清除掉会话cookie，结束浏览器进程才行。

21.标签模板字符串
模板字符串支持在前面添加一个函数，第一个参数是一个有固定内容组成的数组，后面参数依次为传入的变量，函数返回值为模板字符串真正展示的值。不过这个功能个人感觉没啥用。

const tag = (params, ...args) => {
    return params[0] + args[0]; // 返回值为模板字符串的真实值。
}

const str = tag`hello ${'world'}`;
22.字符串常用的几个方法
1. includes();
字符串中是否包含某个字符串，这个不说了，其实就是indexOf的替代方案，用起来更优雅，

2. startsWith();
字符串是否为某个字符串开始，我一般用它判断url是否有http

3. endsWith();
字符串是否为某个字符串结尾。判断后缀名的时候尤其有效。

4. repeat(number);
得到一个重复number次的字符串。额...我也不知道什么时候有用，一般我用它造测试数据。

5. 'abc'.padEnd(5, '1'); // abc11;
用给定的字符串在尾部拼接到指定长度，第一个参数为长度，第二个参数为用于拼接的值。

6. 'abc'.padStart(5, '1'); // 11abc;
用给定的字符串在首部拼接到指定长度第一个参数为长度，第二个参数为用于拼接的值。首部补0？

23.数组快速去重
应该很多人都知道这个，数组转换成Set, 再转换为数组，不过这种去重方式只能去除基本数据类型组成的数组。

const arr = [1, 2, 3, 4, 5, 6];

const arr2 = new Set(arr);

const arr3 = [...arr2];
24.Object.keys, values, entries
一般我们常用Object.keys，返回一个对象的键组成的数组，其实还有Object.values，返回对象值组成的数组，Object.entries将对象转成数组，每个元素是键值对组成的数组，可以使用此功能快速将对象转为Map。


const obj = {name: 'yd', age: 18};

Object.keys(obj); // ['name', 'age'];

Object.values(obj); // ['yd', 18];

const l = Object.entries(obj); // [['name', 'yd'], ['age': 18]];

const m = new Map(l);
25.Object.getOwnPropertyDescriptors
获取对象的描述信息

Object.assign复制时，将对象的属性和方法当做普通属性来复制，并不会复制完整的描述信息，比如this。

const p1 = {
    a: 'y',
    b: 'd',
    get name() {
        return `${this.a} ${this.b}`;
    }
}
const p2 = Object.assign({}, p1);

p2.a = 'z';

p2.name; // y d; 发现并没有修改p2.a的值，是因为this仍旧指向p1
使用Object.getOwnPropertyDescriptors获取完整描述信息

const description = Object.getOwnPropertyDescriptors(p1);

const p2 = Object.defineProperty({}, description);

p2.a = 'z';

p2.name; // z d
26.BigInt
JavaScript可以处理的最大数字是2的53次方 - 1，这一点我们可以在Number.MAX_SAFE_INTEGER中看到。

consoel.log(Number.MAX_SAFE_INTEGER); //9007199254740991
更大的数字则无法处理，ECMAScript2020引入BigInt数据类型来解决这个问题。通过把字母n放在末尾, 可以运算大数据。

BigInt可以使用算数运算符进行加、减、乘、除、余数及幂等运算。它可以由数字和十六进制或二进制字符串构造。此外它还支持AND、OR、NOT和XOR之类的按位运算。唯一无效的位运算是零填充右移运算符。

const bigNum = 100000000000000000000000000000n;
console.log(bigNum * 2n); // 200000000000000000000000000000n

const bigInt = BigInt(1);
console.log(bigInt); // 1n;

const bigInt2 = BigInt('2222222222222222222');
console.log(bigInt2); // 2222222222222222222n;
BigInt是一个大整数，所以他不能用来存储小数。

27.??合并空运算符
假设变量a不存在，我们希望给系统一个默认值，一般我们会使用||运算符。但是在javascript中空字符串，0，false都会执行||运算符，所以ECMAScript2020引入合并空运算符解决该问题，只允许在值为null或未定义时使用默认值。

const name = '';

console.log(name || 'yd'); // yd;
console.log(name ?? 'yd'); // '';
28.?可选链运算符
业务代码中经常会遇到这样的情况，a对象有个属性b,b也是一个对象有个属性c,

我们需要访问c，经常会写成a.b.c，但是如果f不存在时，就会出错。

const a = {
    b: {
        c: 123,
    }
}
console.log(a.b.c); // 123;
console.log(a.f.c); // f不存在所以会报错
ECMAScript2020定义可选链运算符解决该问题，通过在.之前添加一个?将键名变成可选

let person = {};
console.log(person?.profile?.age ?? 18); // 18
29.import
import是ECMAScript2015当中定义的一套ES Module模块系统，语法特性绝大多数浏览器已经支持了，通过给script标签添加type=module的属性就可以使用ES Module的标准去执行javascript代码了。

<script type="module">
console.log('this is es module');
</script>
在ES Module规范下，会采用严格模式(use strict)运行javascript代码。每个ES Module都运行在单独的作用域中，也就意味着变量间不会互相干扰。外部js文件是通过CORS的方式请求的，所以要求我们外部的js文件地址要支持跨域请求，也就是文件服务器要支持CORS。我们可以在任意网站控制台输入下面代码。

const script = document.createElement('script');

script.type = 'module';

script.innerHTML = `import React from 'https://cdn.bootcdn.net/ajax/libs/react/17.0.1/cjs/react-jsx-dev-runtime.development.js';`;

document.body.append(script);
可以发现在network中请求了https://cdn.bootcdn.net/ajax/libs/react/17.0.1/cjs/react-jsx-dev-runtime.development.js资源。

ES Module的script标签会延迟脚本加载，等待网页请求完资源之后才执行，和使用deffer的方式加载资源相同。

需要注意的是，import {} from 'xx'导入模块的时候，并不是对象的解构，而是import的固定语法，这一点很多人容易弄错。

并且ECMAScript2020中import开始支持动态导入功能，在此之前import只能写在模块代码的顶部，一开始就要声明模块依赖的其它模块。支持动态引入后就可以按需引入对应的模块，这个功能我们早在SPA中就已经用到了。动态导入返回的是一个Promise。

a.js

const a = 123;
export { a };
b.js


import('./a.js').then(data => {
    console.log(data.a); // 123;
})
30. 0.1 + 0.2 === 0.3 // false
console.log(0.1+0.2); // 0.30000000000000004
在JS当中，Number类型实际上是double类型，运算小数时存在精度问题。因为计算机只认识二进制，在进行运算时，需要将其他进制的数值转换成二进制，然后再进行计算

小数用二进制表达时是无穷的。

// 将0.1转换成二进制
console.log(0.1.toString(2)); // 0.0001100110011001100110011001100110011001100110011001101

// 将0.2转换成二进制
console.log(0.2.toString(2));  // 0.001100110011001100110011001100110011001100110011001101
双精度浮点数的小数部分最多支持53位二进制位，所以两者相加后，因浮点数小数位的限制而截断的二进制数字，再转换为十进制，就成了0.30000000000000004，这样在进行算术计算时会产生误差。

ES6 在Number对象上面，新增一个极小的常量Number.EPSILON。根据规格，它表示1与大于1的最小浮点数之间的差。对于64位浮点数来说，大于1的最小浮点数相当于二进制的1.00..001，小数点后面有连续51个零。这个值减去1之后，就等于2的-52次方。

Number.EPSILON === Math.pow(2, -52)
// true
Number.EPSILON
// 2.220446049250313e-16
Number.EPSILON.toFixed(20)
// "0.00000000000000022204"
Number.EPSILON实际上是JavaScript能够表示的最小精度。误差如果小于这个值，就可以认为已经没有意义了，即不存在误差了。

引入一个这么小的量的目的，在于为浮点数计算，设置一个误差范围。我们知道浮点数计算是不精确的。

Number.EPSILON可以用来设置能够接受的误差范围。比如，误差范围设为2的-50次方（即Number.EPSILON * Math.pow(2, 2)），即如果两个浮点数的差小于这个值，我们就认为这两个浮点数相等。

(0.1 + 0.2 - 0.3) < Number.EPSILON // true


