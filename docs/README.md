# es6-11与typescripe

## es6+

> 全称EcmaScript,是脚本语言的规范，javascript是EcmaScript的一种实现
>
> ES新特性其实是指javascript的新特性

> 语法简洁，功能丰富
>
> 框架开发应用

### 常量

#### const 常量声明

>1、一定要赋初始值
>2、一般使用大写字母
>3、常量的值不能修改
>4、块儿级作用域
>5、对数组和对象的元素修改，不算修改常量

```javascript
//声明常量
const PI=3.14
const TEAM=['ss','dd','zz']
TEAM.push('gg')
```

### 变量

#### let 变量声明

>let 特性
>1、变量不能重复声明
>2、块儿级作用域 全局，函数，eval
>3、不影响作用域链
>4、不存在变量提升

```javascript
// 声明变量
let a;
let b,c,d;
let e=100;
let f=12,g='123',h=[],i={};
```

点击切换颜色demo

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .item{
            width: 80px;
            height: 60px;
            border:1px solid aquamarine;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2 class="page-header">点击切换颜色</h2>
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
    </div>
    
    <script>
      //获取div元素对象
      let items=document.getElementsByClassName("item");

      //遍历并绑定事件
      for (let i = 0; i < items.length; i++) {
          items[i].onclick=function(){
               //   修改当前元素背景颜色
                //  this.style.background='pink'; //使用var i=0 使用下面的方法会错误，数组越界，var是全局的
               items[i].style.background='pink';
          }          
      }  
    </script>
</body>
</html>
```

#### 变量的解构赋值

> es6允许按照一定模式从数组和对象中提取值，对变量进行赋值，被称为解构赋值

```javascript
//1. 数组的解构
const F4=['小沈阳','刘能','赵四','宋小宝']
let [xsy,ln,zs,sxb] = F4;
console.log(xsy);
console.log(ln);
console.log(zs);
console.log(sxb);

//2. 对象的解构
const ZHAO={
    name:'赵本山',
    age:'不知道',
    xiaopin:function(){
        console.log("我演过小品");
    }
};
let {name,age,xiaopin}=ZHAO; //用变量的名称去匹配属性的名称，然后进行赋值
console.log(name);
console.log(age);
console.log(xiaopin);
xiaopin();
let {xiaopin:xp}=ZHAO; //在冒号左边的是用于属性的匹配，冒号右边的才是真正的赋值
```

### 模板字符串

>特性
>
>1、可以直接出现换行符
>
>2、变量拼接

```javascript
// es6声明字符串的方式 ``,'',""
let love="爱你";
// 声明模板字符串
let str=`字符串`;
let str1=`<ul>
			<li>1</li>
		  </ul>
`;
let str2=`${love}哈哈`;
```

### 对象的简化写法

> 允许在{}里面，直接写入变量和函数，作为对象的属性和方法
>
> 这样写更简洁

```javascript
let name="haha";
let change=function(){
    console.log('改变你');
}

const SCHOOL={
    name, // 完整写法：name:name
    change,// 完整写法：change:change
    improve(){
        console.log("提高");
    },//完整写法：improve:function(){}
}
```

### 箭头函数

> 使用=>定义函数
>
> 箭头函数适用于与this无关的回调，定时器，数组的方法回调
>
> 不适合与this有关的回调，时间回调，对象的方法

```javascript
//声明一个函数
let fn=(a,b)=>{return a+b;}

//注意this的指向
//1. this是静态的，this始终指向函数声明时所在作用域下的this的值
function getName(){
    console.log(this.name);
}
let getName2=()=>{
    console.log(this.name);
}

//给window对象设置name属性
window.name="哈哈";
const SCHOOL={
    name:"SCHOOL"
}
//直接调用
getName();//输出哈哈
getName2();//输出哈哈

//call函数调用
getName.call(SCHOOL); //输出SCHOOL
getName2.call(SCHOOL); //输出哈哈

//2. 不能作为构造函数实例化对象
let Person=(name,age)=>{this.name=name;this.age=age;}
let me=new Person('zs',13);  //报错

//3. 不能使用arguments 变量
let fn=()=>{
    console.log(arguments);
}
fn(1,2,3); //报错

//4. 箭头函数的简写
// 1)省略(),当形参只有一个时
// 2)省略{},代码题只有一条语句时，此时return必须省略，执行结果就是返回结果
```

demo

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div{
            width: 80px;
            height: 60px;
            background-color: aqua;
        }
    </style>
</head>
<body>
    <div id="ad">
       
    </div>
    
    <script>
        //点击div 2秒后变成粉色
        let ad=document.getElementById('ad');
        //绑定事件
        ad.addEventListener('click',function(){
            let _this=this;
            //定时器
            setTimeout(function() {
                // 不在定时器外保存this，this指向window,没有style属性
                _this.style.background='pink';
            }, 2000);
        });
        //使用箭头函数
        ad.addEventListener('click',function(){
            setTimeout(() => {
                this.style.background='pink'; 
            }, 2000);
        });
    </script>
</body>
</html>
```

### 函数参数默认值

```javascript
//1.形参初始值(一般赋初始值的参数靠后)
function add(a,b,c){
    return a+b+c;
}
let result=add(1,2);
console(result);//输出NAN

function add(a,b,c=3){
    return a+b+c;
}
let result=add(1,2);
console(result);//13

//2.与解构赋值结合
function connect({hoat='127.0.1',username,password}){ //解构赋值+默认值
    let []
}
connect({
    host:'localhost',
    username:'root',
    password:'root',
})
```

### rest参数

> es6引入rest参数，用于获取函数的实参，代替arguments
>
> rest 参数必须放在参数最后，是一个数组
>
> 貌似有点java可变参数，哈哈

```javascript
//es5获取实参的方式
function data(){
    console.log(arguments);
}
data('拉了','和嘎嘎');

//使用rest参数
function date(...args){
    console.log(args);
}
```

### 扩展运算符

> 将数组转换为逗号分隔的参数序列
>
> 貌似有点python的*args实参，哈哈

```javascript
const Team=['aa','bb','cc'];
function member(){
    console.log(arguments);
}
//使用扩展运算符
member(...Team);//member('aa','bb','cc')
```

demo

```javascript
//1.数组的合并
const A=['1','2'];
const B=['3','4'];
const AB=[...A,...B];
//2. 数组的clone
const C=[...AB];//浅copy

//3.伪数组转为真正的数组
const divs=document.querySelectorAll('div');
const divArr=[...divs];

```

#### reset参数与扩展运算符

```javascript
function connect({host,port,...user}){
    console.log(host);
    console.log(port);
    console.log(user);
}
connect({
    host:'127.0.0.1',
    port:3306,
    username:'root',
    password:'root'
})

const skillone={
    q:'q'
}
//...skillone ==>q:'q'
const skilltwo={
    f:'f'
}
const skill={...skillone,...skilltwo} 
```

### Symbol

> es6新的原始数据类型，表示独一无二的值，类似于字符串
> Symbol的值是唯一的，解决命名冲突
> Symbol值不能与其他数据进行运算
> Symbol定义的对象属性不能使用for...in 循环遍历，可以使用Reflect.ownKeys获取对象的所有键名

#### 内置属性

> **Symbol.hasInstance**
>**Symbol.isConcatSpreadable**
> **Symbol.species**
> **Symbol.match/replace/search/split**
> **Symbol.iterator**
> 
> 定义一个对象的遍历器方法。凡是具有[Symbol.iterator]方法的对象都是可遍历的，可以使用for … of循环依次输出对象的每个属性

```javascript
//创建Symbol
//1.Symbol()
let s1=Symbol();

let s2=Symbol('描述字符串');//传入的值可以理解为注释，不能通过描述字符串得到唯一值

//2.Symbol.for()  可以通过描述字符串得到唯一值
let s3=Symbol.for('aa');
let s4=Symbol.for('bb');
console.log(s3===s4);//true
```

demo

```javascript
//向对象中添加方法，up,down
let game={......} //里面有超多值
//声明对象
let methods={
 	up:Symbol(),
    down:Symbol(),
};
game[methods.up]=function(){
    console.log("up");
};
game[methods.down]=function(){
    console.log("down");
}
let play={
    name:'狼人杀',
    [Symbol('say')]:function(){},
    
}
```

#### 获取描述字符串

> Symbol.prototype.description

```javascript
//创建Symbol
let s=Symbol('name');
//获取name
console.log(s.description);
```

### 迭代器

> 部署Iterator接口，完成遍历操作
>
> es6   for...of
>
> 原生具备iterator接口的数据
>
> ​	Array
>
> ​	Arguments
>
> ​	Set
>
> ​	Map
>
> ​	String
>
> ​	TypedArray
>
> ​	NodeList

### 生成器

```javascript
function * gen(){
    yield 'lala';
}
let iterator=gen();
iterator.next();
```

> 解决回调地狱
>
> ```javascript
> function one(){
>  setTimeout(()=>{
>      console.log(111)
>      iterator.next();
>  },2000)
> }
> function two(){
>  setTimeout(()=>{
>      console.log(222)
>      iterator.next();
>  },2000)
> }
> function three(){
>  setTimeout(()=>{
>      console.log(333)
>  },2000)
> }
> 
> //生成器函数
> function * gen(){
>  yield one();
>  yield one();
>  yield three();
> }
> 
> //调用生成器
> let iterator=gen();
> iterator.next();
> ```

> 管理关联数据
>
> ```javascript
> function user(){
>  setTimeout(()=>{
>      let data="用户数据";
>      iterator.next(data);
>  },2000)
> }
> function order(){
>  setTimeout(()=>{
>      let order="订单数据";
>      iterator.next(order);
>  },2000)
> }
> function product(){
>  setTimeout(()=>{
>      let product="商品数据";
>       iterator.next(product);
>  },2000)
> }
> 
> //生成器函数
> function * gen(){
>  let users=yield user();
>  let orders=yield roder();
>  let products=yield product();
> }
> ```

### Promise

> 异步编程新方案
>
> 是一个构造函数，用来封装异步操作可以获取其成功或失败的结果
>
> 1）Promise构造函数：Promise(excutor){}
>
> 2)Promise.prototype.then方法
>
> 3）Promise.prototype.catch方法

```javascript
//实例化Promise对象
const p=new Promise(function(resolve,reject){
    setTimeout(function(){
        let data="数据库中的数据";
        resolve(data);//调用resolve()后p对象的状态变为成功
        //若读取数据失败
        let err="失败";
        reject(err);//调用 reject()后p对象的状态变为失败
    },1000)
});

//调用promise对象的then方法
p.then(function(value){
    //状态成功，调用此方法
    console.log(value);//数据库中的数据
},function(reason){
    //状态失败，调用此方法
    console.log(reason);//失败
})
```

> 封装Ajax
>
> ```javascript
> const p=new Promise((resolve,reject)=>{
>  //1.创建对象
> 	const xhr=new XMLHttpRequest();
> 	//2.初始化
> 	xhr.open("get","接口地址");
> 	//3.发送
> 	xhr.send();
> 	//4.绑定事件，处理结果
> 	xhr.onreadystatechange=function(){
>  	//判断
>  	if(xhr.readystate === 4){
>     	 	//判断响应码
>      	if(xhr.status>=200 && xhr.status<=300){
>              //成功
>         	 	//console.log(xhr.response);
>              resolve(xhr.response);
>      	}else{
>          	//失败
>          	//console.error(xhr.status);
>              reject(xhr.status);
>      	}
> 	  }
> 	}
> });
> //指定回调
> p.then(function(value){
>  console.log(value);
> },function(reason){
>  console.log(reason);
> });
> ```

> catch方法
>
> ```javascript
> p.catch(function(reason){
>  console.warn(reason);
> });
> ```

#### allsettled与all

> allsettled 返回的状态为成功，值中包含状态和返回的值
>
> all 数组中的状态全部成功才返回成功的Promise

```javascript
//声明两个Promise对象
const p1=new Promise((resolve,reject)=>{
setTimeout(()=>{
  resolve('数据---1');
},1000)
});
const p2=new Promise((resolve,reject)=>{
setTimeout(()=>{
  resolve('数据---2');
},1000)
});
//调用allsettled方法
const result=Promise.allSettled([p1,p2]);
console.log(result)
```

### 集合Set

```javascript
//声明一个集合
let s=new Set();
let s2=new Set(['1','1','2']) //传入一个可迭代对象，自动去重

console.log(s2.size) //元素个数
s2.add('3') //添加元素
s2.delete('2') //删除元素
s2.has('1') //检测元素
s2.clear() //清空元素
//遍历
for(let v of s2){
    console.log(v)
}
```

集合的应用

```javascript
let arr=[1,1,2,3,3,4,5,5,6]
//1. 集合去重
let a1=[...new Set(arr)];
//2. 求交集
let arr2=[3,4,7,8]
let a2=[...new Set(arr)].filter(item=>{
    let s2=new Set(arr2);
    if(s2.has(item)){
        return true
    }else{
        return false
    }
})
//简化
let a2=[...new Set(arr)].filter(item=>new Set(arr2).has(item));
//3. 求并集
let union=[...new Set([...arr,...arr2])];
//4. 求差集
let diff=[...new Set(arr)].filter(item=>!(new Set(arr2).has(item)));
```

### Map

```javascript
//声明
let m=new Map();

//添加元素 键值对可以是各种类型
m.set('name','张三');
m.set("change",function(){
    console.log("change")
});
let key={country:"china"}
m.set(key,['北京','上海']);

//删除
m.delete('name')  # 根据key删除

//获取
m.get(key)

//清空
m.clear()

//遍历
for(let v of m){
    console.log(v)
}
```

### class

es5定义一个类

```javascript
function Phone(brand,price){
    this.brand=brand;
    this.price=price;
}
//添加方法
Phone.prototype.call=function(){
    console.log("我可以打电话");
}

//实例化对象
let huawei=new Phone('华为',5999);
huawei.call();
```

es6定义一个类

```javascript
class Phone{
    //构造方法
    constructor(brand,price){
        this.brand=brand;
    	this.price=price;
    }
    call(){console.log("我可以打电话");}
}
let oneplus=new Phone('1+',5399);
oneplus.call();
```

静态成员

> 属于类，不属于实例对象

```javascript
class Phone{
    static name='手机';
    static change(){
        console.log("世界被我改变")
    }
}
let =new Phone();

console.log(p.name);//undifined
console.log(Phone.name);//手机
```

继承

```javascript
class Phone{
    constructor(brand,price){
        this.brand=brand;
    	this.price=price;
    }
    call(){console.log("我可以打电话");}
}

class SmartPhone extends Phone{
    constructor(brand,price,color,size){
        super(brand,price);
        this.color=color;
        this.size=size;
    }
    playGame(){ 
       console.log("我可以打游戏"); 
    }
}
let sp=new SmartPhone('华为',5999,'白色','15');
```

重写父类方法

​	重名方法调用子类的

getter和setter

> 当调用或设置属性时，会调用对应的get和set函数

```javascript
class Phone{
    get price(){
        console.log("价格被读了");
        return '15';
    }
    set price(newVal){
        console.log("价格被设置了");
    }
}

let p=new Phone();
console.log(p.price);
s.price='free';
```

对象扩展方法

判断两个值是否相等

> Object.is() 
>
> 类似于===但不完全等于
>
> ```javascript
> console.log(Object.is(12,120)) //false
> console.log(Object.is(NaN,NaN)) //true
> console.log(NaN===NaN) //false
> ```

对象的合并

> Object.assign()
>
> 重复的属性会被后一个对象覆盖
>
> ```javascript
> const config1={
> host:'localhost',
> port:3306,
> name:'root',
> pass:'root'
> };
> const config2={
> host:'http://www.baidu.com',
> port:33060,
> name:'admin',
> pass:'admin'
> };
> Object.assign(config1,config2)
> ```

设置原型对象

> Object.setPrototypeOf()
>
> ```javascript
> const school={
> name:'学习'
> }
> const cities={
> city:['beijing','shanghai']
> }
> Object.setPrototypeOf(school,cities);
> ```
>
> 获取原型对象
>
> Object.getPrototypeOf()

### 模块化

> 将大的程序文件拆分成许多小的文件，然后组合起来
>
> 优点：
>
> ​	防止命名冲突
>
> ​	代码复用
>
> ​	高维护性

模块功能主要由export和import构成

- export 用于规定模块的对外接口
- import 输入其他模块提供的功能

> demo
>
> ​	导出
>
> ```javascript
> m1.js文件
> //分别暴露
> export let school='xuexiao';
> export function teach(){
> console.log('教书')
> }
> ```
>
> ```javascript
> //统一暴露
> let school='xuexiao';
> function teach(){
> console.log('教书')
> };
> export {
> school,teach
> };
> ```
>
> ```javascript
> //默认暴露,可以是任意类型，一般以对象居多
> export default{
> school:'学习',
> change:function(){
>   console.log("改变");
> }
> }
> ```
>
> ​	导入
>
> ```html
> html文件
> <!DOCTYPE html>
> <html lang="en">
> <head>
> <meta charset="UTF-8">
> <meta http-equiv="X-UA-Compatible" content="IE=edge">
> <meta name="viewport" content="width=device-width, initial-scale=1.0">
> <title>es6</title>
> </head>
> <body>
> <script type="module">
>   //通用导入
>   import * as m1 from "m1.js";
>   console.log(m1)
> </script>
> </body>
> </html>
> ```
>
> ```html
> <script type="module">
> //解构赋值形式
> import {school as myschool,teach} from "m1.js";
> console.log(myschool);
> console.log(teach);
> //解构导入默认暴露
> import {deafult as m2} from 'm1.js';
> //针对默认暴露的简便形式
> import m2 from 'm1.js';
> </script>
> ```

bable对es6模块化代码转化

> 转换成浏览器直接识别的es5文件

安装工具

bable-cli  bable的命令行工具

bable-preset-env  将es6转换成es5

browserify（与webpack作用相同） 打包工具

```shell
npm i babel-cli babel-preset-env browserify -D
```

转化

> 将js目录下的文件转化到dist/js目录下

```shell
npx babel src/js -d dist/js --presets-babel-preset-env
```

打包

> app.js为模块化的入口文件

```shell
npx browserify dist/js/app.js -o dist/bundle.js
```

### async 和await

> async 和await两种语法结合可以让异步代码像同步代码一样

#### async函数

async函数的返回值为promise对象

promise对象的结果由async函数执行的返回值决定

> 这个函数返回的结果不是一个Promise类型对象，返回成功的Promise对象
>
> 抛出错误，返回的结果是一个失败的Promise
>
> 返回的结果是一个Promise对象，返回对应的值

#### await表达式

await必须写在async函数中

await 右侧的表达式一般为promise对象

await返回的是promise成功的值

await的promise失败了，就会抛出异常，需要通过try...catch捕获处理

```javascript
//创建Promise对象
const p=new Promise((resolve,reject)=>{
    resolve("成功");
})

async function main(){
    try{
        let result=await p;
        console.log(result);
    }catch(e){
       console.log(e);
    }
//调用函数
main();
}
```

##### 读取文件

```javascript
//首先node 安装fs 模块
//引入fs模块
const fs = require("fs");
//读取文件
function readMyFile1(){
    return new Promise((resolve,reject)=>{
        fs.readFile("file1path",(err,data)=>{
            //如果读取失败
            if(err) reject(err);
            resolve(data);
        })
    })
}
function readMyFile2(){
    return new Promise((resolve,reject)=>{
        fs.readFile("file2path",(err,data)=>{
            //如果读取失败
            if(err) reject(err);
            resolve(data);
        })
    })
}

//定义async函数
async function main(){
    let f1=await readMyFile1();
    let f2=await readMyFile2();
    
    console.log(f1.toString());
    console.log(f2.toString());
}
main();
```

##### Ajax请求

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <script>
        //发送AJAX请求，返回结果是Promise对象
        function sendAJAX(url) {
            return new Promise((resolve, reject) => {
                //1.创建对象
                const x = new XMLHttpRequest();
                //2.初始化
                x.open("GET", url);
                //3.发送
                x.send();
                //4.绑定事件
                x.onreadystatechange = function () {
                    if (x.readyState === 4) {
                        if (x.status >= 200 && x.status < 300) {
                            resolve(x.response);
                        } else {
                            reject(x.status);
                        }
                    }
                }
            })
        }

        //测试Promise对象
        // sendAJAX("https://api.apiopen.top/api/sentences").then(value => console.log(value), response => console.log(response))
        
        // 测试async和await
        async function main(){
            //直接拿结果，nice
            let result=await sendAJAX("https://api.apiopen.top/api/sentences");
            console.log(result)
        }
        main()
    </script>
</body>

</html>
```

### 私有属性

> 变量前加#

```javascript
class Person{
//公有属性
name;
//私有属性
#age;
#weight;
//构造方法
constructor(name,age,weight){
  this.name=name;
  this.#age=age;
  this.#weight=weight;
}
getAge(){
  console.log(this.#age)
}
}
//实例化
const gril=new Person('红红',18,'45kg');
console.log(gril.name); //正常访问
console.log(gril.#age); //不能访问
gril.getAge();//访问#age成功
```



### 扩展

#### 指数运算符**

> 与Math.pow结果相同

```javascript
//**
console.log(2**10);
console.log(Math.pow(2,10));
```

#### 字符串扩展方法

> 在trim方法的基础上扩展了

##### trimStart与trimEnd

```javascript
let srt="  i love u";
str.trimStart();//清除左侧字符
str.trimEnd();// 清除右侧字符
```

##### matchAll

> String.prototype.matchAll

```javascript
let str=`
<ul>
	<li>
		<a>1</a>
		<p>2</p>
	</li>
	<li>
		<a>1</a>
		<p>2</p>
	</li>
</ul>
`;

const reg=/<li>.*?<a>(.*?)<\/a>.*?<p>(.*?)<\/p>/gs;
const result=str.matchAll(reg);
//for(let v of result){
//  console.log(v);
//}
const arr=[...result];
console.log(arr);
```

#### 可选链操作符

> ?.
>
> 免去层层判断
>
> ```javascript
> function main(config){
> //const dbHost=config && config.db &&config.bd.host
> const dbHost=config?.db?.host; 
> console.log(dbHost);
> }
> //main();
> main({
> db:{
>   host:"192.168.1.100",
>   username:'root'
> },
> cache:{
>   host:"192.168.1.200",
>   username:'admin'  
> }
> })
> ```

#### 动态import

> import()

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <button id="btn">点击</button>
    <script type="module" src="./app.js">

    </script>
</body>
</html>
```

app.js

```javascript
// import * as m1 from './hello.js' 静态导入
const btn=document.getElementById("btn");
btn.onclick=function(){
    import('./hello.js').then(m1=>{
        m1.hello();
    })
}
```

hello.js

```javascript
export function hello(){
    alert("hello");
}
```

#### BigInt类型

> 普通的int类型后加n
>
> 函数BigInt
>
> ```javascript
> let n=123n;
> console.log(n,typeof(n));
> 
> let n1=123;
> console.log(BigInt(n1));
> ```

#### globalThis

> 始终指向全局对象

```javascript
console.log(this)
console.log(globalThis)
```

#### 数组

##### 数组中是否包含某元素

> Array.prototype.includes

```javascript
//includes
const array=['1','2'];
console.log(array.includes('1'))
```

##### 将高维数组转为低维数组

```javascript
//flat 将高维数组转为低维数组
const arr=[1,2,3,4,[5,6,7,[8,9]]]
//参数为深度
arr.flat();//arr为三维降为二维，为二维降为一维
arr.flat(2);//arr为三维降为一维

//flatMap
const arr1=[1,2,3,4];
const result=arr1.map(item=>[item*10]);
console.log(result); //变成了二维数组
arr1.flatMap(item=>[item*10]);//flat与map的结合
```



#### 对象

##### 获取对象的所有key

> Object.keys

##### 获取对象的所有value

> Object.values

##### 将对象的属性转成数组

> Object.entries

##### 将键值对类型转成对象

> Object.fromEntries

```javascript
//es8
const arr=Object.entries({
name:'学习'
})
//es10
const result=Object.fromEntries(arr)

const m=new Map()
m.set('name','学校')
const result1=Object.fromEntries(m)
```



##### 获取对象属性描述对象

> Object.getOwnPropertyDescriptors

```javascript
const school={
    name:'学校',
    cities:['北京','上海']
};
console.log(Object.keys(school));
console.log(Object.values(school));
const arr=Object.entries(school);
console.log(arr);
//创建map
const map=new Map(arr);
console.log(map);
//创建对象
const obj=Object.create(null,{
    name:{
        //设置值
        value:'尚硅谷',
        //属性特性
        writable:true,
        configurable:true,
        enumerable:true
    }})
console.log(Object.getOwnPropertyDescriptors(obj));
```

#### 正则扩展

##### 命名捕获分组

> ?<名字>

```javascript
//声明一个字符串
let str='<a href="http://www.baidu.com">百度</a>'
//提取url和标签文本
const reg=/<a href="(.*)">(.*)<\/a>/;
//执行
const result=reg.exec(str);
console.log(result);
console.log(result[1]);
console.log(result[2]);

//命名捕获分组
const reg=/<a href="(?<url>.*)">(?<text>.*)<\/a>/;
const result=reg.exec(str);
console.log(result.groups.url);
console.log(result.groups.text);
```

##### 反向断言

```javascript
let str='js122345你好555啦啦';
//正向断言,获取555
const reg=/\d+(?=啦)/;
const result=reg.exec(str);
console.log(result);
//反向断言
const reg=/(?<=好)\d+/;
const result=reg.exec(str);
console.log(result);
```

##### dotAll模式

> dot "."元字符 除换行符以外的任意单个字符
>
> ```javascript
> let str=`
> <ul>
> 	<li>
> 		<a>1</a>
> 		<p>2</p>
> 	</li>
> 	<li>
> 		<a>1</a>
> 		<p>2</p>
> 	</li>
> </ul>
> `
> //const reg=/<li>\s+<a>(.*?)<\/a>\s+<p>(.*?)<\/p>/;//普通模式
> const reg=/<li>.*?<a>(.*?)<\/a>.*?<p>(.*?)<\/p>/gs;
> let result;
> while(result=reg.exec(str)){
> console.log(result);
> }
> console.log(result);
> ```

## typescript

> 解决js的一些缺点，是扩展的javascript
>
> 需要编译成js才能被解析

### 开发环境搭建

安装node.js

全局安装typescript

```shell
npm i -g typescript
```

编译ts文件

```shell
# 进入ts文件所在目录
tsc xxx.ts
```

### 基本类型

> 在定义变量时，给定类型后，不能赋值其他类型的值

种类

> any 可以赋值给任何类型，unknown不能直接赋值给其他类型

| 类型    | 例子            | 描述                           |
| ------- | --------------- | ------------------------------ |
| number  | 1,-33,2.5       | 任意数字                       |
| string  | 'hi', "hi", hi  | 任意字符串                     |
| boolean | true、false     | 布尔值true或false              |
| 字面量  | 其本身          | 限制变量的值就是该字面量的值   |
| any     | *               | 任意类型                       |
| unknown | *               | 类型安全的any                  |
| void    | 空值(undefined) | 没有值（或undefined)           |
| never   | 没有值          | 不能是任何值                   |
| object  | {name:孙悟空}   | 任意的JS对象                   |
| array   | [1,2,3]         | 任意JS数组                     |
| tuple   | [4,5]           | 元素，TS新增类型，固定长度数组 |
| enum    | enum{A, B}      | 枚举，TS中新增类型             |

格式

> 变量/参数/函数:类型

```typescript
let a:number;
let b=false;
let c:boolean=true;
//字面量
let d:10;
let e='meal'|'femeal';
a=10;
a="hello";//此行代码会报错
d=10;//ok
d=11//报错
let f:unknown;
let g:string;
f='123';
if(typeof f==="string"){ //类型判断后赋值给其他类型
   g=f 
}
//类型断言，可以用来告诉解析器实际的变量类型
g=f as string;
s=<string>e;//等同于上面


function sum(a:number,b:number):number{//参数类型与函数返回值类型
    return 
}
function f1():never{//表示永远不会返回结果
    throw new Error("报错了");
}

let h:(number,number)=>number;
h=function(n1,n2):number{
    return n1+n2;
}
```

### 可选属性

> 属性名后加？

```typescript
let b:{name:string,age?:number};
b={name:'孙'}
b={name:'孙',age:18}//age就是一个可选属性
//[propName:String]:any表示任意类型的属性，propName 随便起的
let c:{name:string,[propName:string]:any}
c={name:'sun',sex:1}
```

### 类型别名

> type MyType=string
>
> type Mytype=1|2|3|4|5
>
> ```typescript
> type MyType=string;
> let a:MyType='1';
> 
> type Mytype1=1|2|3|4|5;
> let b:MyType1;
> b=1;
> ```

### TS编译选项

#### 自动编译

> 监视ts文件的变化

```shell
-w
# tsc -w app.ts
```

#### 自动编译整个项目

前提

> 在项目下新建一个tsconfig.json文件
>
> ```json
> {
> 
> }
> ```
>
> 

命令行

```shell
# 进入项目目录
tsc # 自动编译所有ts文件
tsc -w # 监视所有文件
```

#### tsconfig.json文件的配值

```json
{
    /*
    tsconfig.json是ts编译器的配置文件，可以根据他的配置信息对代码编译
    */
    
}
```

##### 配置选项

###### 编译文件

- include

  ```json
  {
      /* 指定哪些ts文件需要被编译，默认编译项目下所有文件
       **表示任意目录
       * 表示任意文件
      */
      "include":["./src/**/*"]
  }
  ```

- exclude

  ```json
  {
      /* 指定哪些ts文件不需要被编译
      默认值：[ "node_modules", "bower_components ", "jspm_packages"]
      */
      "exclude":["./src/hello/**/*"]
  }
  ```

- extends

  ```json
  {
      //定义被继承的配置文件
      "extends":"./config/base"
  }
  ```

- files

  ```json
  {
      //指定需要被编译的文件
      "files":[
          "xx.ts",
          "cc.ts",
      ]
  }
  ```

###### 编译器选项

- compilerOptions

  > 编译器的选项

  - target

    > 用来指定ts被编译的js版本，默认就是es3

    ```json
    {
        "compilerOptions":{
            "target":"ES3"
        }
    }
    ```

  - module

    > 指定模块化的规范

    ```json
    {
        "compilerOptions":{
            "module":"es2015"
        }
    }
    ```

  - lib

    > 指定项目中要使用的库

    ```json
    {
        "compilerOptions":{
            "lib":["dom"] //一般不需要设置
        }
    }
    ```

  - outDir

    > 用来指定编译后文件所放目录

    ```json
    {
        "compilerOptions":{
            "outDir":"./dist"
        }
    }
    ```

  - outFile

    > 将所有全局作用域中的代码合并到同一个文件

    ```json
    {
        "compilerOptions":{
            "outFile":"./dist/app.js"
        }
    }
    ```

  - allowJs

    > 是否对js文件进行编译,默认false

    ```json
    {
        "compilerOptions":{
            "allowJs":false
        }
    }
    ```

  - checkJs

    > 是否检查js语法符合规范,默认false

    ```json
    {
        "compilerOptions":{
            "checkJs":false
        }
    }
    ```

  - removeComments

    > 编译js是否移除注释

    ```json
    {
        "compilerOptions":{
            "removeComments":true
        }
    }
    ```

  - noEmit

    > 不生成编译后的文件

    ```json
    {
        "compilerOptions":{
            "noEmit":true
        }
    }
    ```

  - noEmitOnError

    > 当有错误时，不生成编译文件

    ```json
    {
        "compilerOptions":{
            "noEmitOnError":true
        }
    }
    ```

###### 语法检查

- compilerOptions

  - alwaysStrict

    > 设置编译后的文件是否使用严格模式，默认false

    ```jsom
    {
        "compilerOptions":{
            "alwaysStrict":true
        }
    }
    ```

  - noImplicitAny

    > 不允许隐式any

    ```json
    {
        "compilerOptions":{
            "noImplicitAny":true
        }
    }
    ```

  - noImplcitThis

    > 不允许不明确类型的this

    ```json
    {
        "compilerOptions":{
            "noImplcitThis":true
        }
    }
    ```

  - strictNullChecks

    > 严格检查空值

    ```json
    {
        "compilerOptions":{
            "strictNullChecks":true
        }
    }
    ```

  - strict

    > 所有严格检查的总开关

    ```json
    {
        "compilerOptions":{
            "strict":true
        }
    }
    ```

### 使用webpack打包ts

#### 项目初始化

> 生成package.json

```shell
npm init -y
```

#### 安装webpack

```shell
npm install -D webpack webpack-cli typescript ts-loader
```

#### 使用

创建webpack.config.js

```javascript
const path=require('path');
//webpack中的所有配置信息都应写在module.exports中
module.exports={
    //指定入口文件
    entry:"./src/index.ts",
    //指定打包文件所在目录
    output:{
        //指定打包文件的目录
        path:path.resolve(__dirname,'dist'),
        //打包后文件的文件名
        filename:"bundle.js"
    },
    //指定打包时要用的模块
    module:{
        //指定要加载的规则
        rules:[
            {
                //test指定规则生效的文件
                test:/\.ts$/,
                //要使用的loader
                use:'ts-loader',
                //要排除的文件
                exclude:/node-modules/,
            }
        ]
    }
}
```

创建tsconfig.json

打包配置

package.json

```json
{
    "scripts":{
        "build":"webpack"
    }
}
```

#### 打包

```shell
npm run build
```

##### 自动生成html文件

```shell
npm i -D html-webpack-plugin
```

在webpack.config.js中引入

```javascript
const path=require('path');
//引入html插件
const HTMLWebpackPlugin=require('html-webpack-plugin');
//webpack中的所有配置信息都应写在module.exports中
module.exports={
    //指定入口文件
    entry:"./src/index.ts",
    //指定打包文件所在目录
    output:{
        //指定打包文件的目录
        path:path.resolve(__dirname,'dist'),
        //打包后文件的文件名
        filename:"bundle.js"
    },
    //指定打包时要用的模块
    module:{
        //指定要加载的规则
        rules:[
            {
                //test指定规则生效的文件
                test:/\.ts$/,
                //要使用的loader
                use:'ts-loader',
                //要排除的文件
                exclude:/node-modules/,
            }
        ]
    },
    //配置html插件
    plugins:[
        new HTMLWebpackPlugin(),
        /*
        自定义属性
        new HTMLWebpackPlugin(
        {
        //title:"这是一个自定义title",
        template:"./src/index.html",//根据模板文件生成
        }
        ),
        */
    ]
};
```

##### css处理插件(less)

```shell
npm i -D less less-loader css-loader style-loader
```

```shell
npm i -D postcss postcss-loader postcss-preset-env
```

```typescript
const path=require('path');
//引入html插件
const HTMLWebpackPlugin=require('html-webpack-plugin');
//webpack中的所有配置信息都应写在module.exports中
module.exports={
    //指定入口文件
    entry:"./src/index.ts",
    //指定打包文件所在目录
    output:{
        //指定打包文件的目录
        path:path.resolve(__dirname,'dist'),
        //打包后文件的文件名
        filename:"bundle.js"
    },
    //指定打包时要用的模块
    module:{
        //指定要加载的规则
        rules:[
            {
                //test指定规则生效的文件
                test:/\.ts$/,
                //要使用的loader
                use:'ts-loader',
                //要排除的文件
                exclude:/node-modules/,
            },
            {
                test:/\.less$/,
                use:[
                    "style-loader",
                    "css-loader",
                    {
                        loader:"postcss-loader",
                        options:{
                            postcssOptions:{
                                plugins:[
                                    "postcss-preset-env",
                                    {
                                        browsers:"last 2 versions"
                                    }
                                ]
                            }
                        }
                    }
                    "less-loader"
                ]
            }
        ]
    },
    //配置html插件
    plugins:[
        自定义属性
        new HTMLWebpackPlugin(
        {
        template:"./src/index.html",//根据模板文件生成
        }
        ),
    ]
};
```



##### 自动运行项目

```shell
npm i -D webpack-dev-server
```

在package.json

```json
{
    "scripts":{
        "build":"webpack",
        //配置用chrome浏览器打开
        "start":"webpack serve --open chrome.exe"
    }
}
```

运行

```shell
# 终端
npm start
# 或 点击start右端的运行符
```

##### 编译前清空dist目录

```shell
npm i -D clean-webpack-plugin
```

webpack.config.json

```json
const path=require('path');
//引入html插件
const HTMLWebpackPlugin=require('html-webpack-plugin');
//引入clean
const {CleanWebpackPlugin} =require('clean-webpack-plugin')
//webpack中的所有配置信息都应写在module.exports中
module.exports={
    //指定入口文件
    entry:"./src/index.ts",
    //指定打包文件所在目录
    output:{
        //指定打包文件的目录
        path:path.resolve(__dirname,'dist'),
        //打包后文件的文件名
        filename:"bundle.js"
    },
    //指定打包时要用的模块
    module:{
        //指定要加载的规则
        rules:[
            {
                //test指定规则生效的文件
                test:/\.ts$/,
                //要使用的loader
                use:'ts-loader',
                //要排除的文件
                exclude:/node-modules/,
            }
        ]
    },
    //配置html插件
    plugins:[
        new HTMLWebpackPlugin(
        {
        template:"./src/index.html",//根据模板文件生成
        }
        ),
        //配置清空插件
     	new CleanWebpackPlugin()
    ],
    //引入模块配置
    resolve:{
        extensions:['.ts','.js']
    }
};
```

#### babel

> js编译器，编译成其他版本

安装

```shell
npm i -D @babel/core @babel/preset-env babel-loader core-js
```

配置webpack

```js
const path=require('path');
//引入html插件
const HTMLWebpackPlugin=require('html-webpack-plugin');
//引入clean
const {CleanWebpackPlugin} =require('clean-webpack-plugin')
//webpack中的所有配置信息都应写在module.exports中
module.exports={
    //指定入口文件
    entry:"./src/index.ts",
    //指定打包文件所在目录
    output:{
        //指定打包文件的目录
        path:path.resolve(__dirname,'dist'),
        //打包后文件的文件名
        filename:"bundle.js",
        //告诉webpack不使用箭头函数（ie11不支持箭头函数）
        environment:{
            arrowFunction:false
        }
    },
    //指定打包时要用的模块
    module:{
        //指定要加载的规则
        rules:[
            {
                //test指定规则生效的文件
                test:/\.ts$/,
                //要使用的loader,从后往前执行
                use:[{
                    //指定加载器
                    loader:'babel-loader',
                    //设置babel
                    options:{
                        //设置预定义的环境
                        presets:[
                            [
                                //指定环境的插件
                                "@babel/preset-env",
                                //配置信息
                                {
                                    targets:{
                                        "chrome":"88"
                                    },
                                    "corejs":"3",//这里下载的3版本，指定为3
                                    //使用corejs的方式“usage”,表示按需加载
                                    "useBuiltIns":"usage"
                                }
                            ]
                        ]
                    }
                },'ts-loader'],
                //要排除的文件
                exclude:/node-modules/,
            }
        ]
    },
    //配置html插件
    plugins:[
        new HTMLWebpackPlugin(
        {
        template:"./src/index.html",//根据模板文件生成
        }
        ),
        //配置清空插件
     	new CleanWebpackPlugin()
    ],
    //引入模块配置
    resolve:{
        extensions:['.ts','.js']
    }
};
```

### 面向对象

#### 类

```typescript
class Person{
//定义实例属性
name:string="张三";
//定义只读属性
readonly sex:string="男"
//定义static属性
static age:number=18;

//定义实例方法
sayHello(){
    console.log("hello")
}
//定义静态方法
static getAge(){
    console.log(this.age)
}

}

const per=new Person();
console.log(per)
```

构造方法

```typescript
class Dog{
    name:string;
    age:number;
    //构造函数，new对象时执行
    constructor(name:string,age:number){
        //设置实例属性,this代表当前实例对象
        this.name=name;
        this.age=age;
    }
    bark(){
        console.log("汪汪")
    }
}
```

继承

```typescript
(function(){
    //在立即执行函数中，避免名称检查冲突
    class Animal{
        name:string;
        age:number;
        constructor(name:string,age:number){
            this.age=age;
            this.name=name;
        }
        sayHello(){
            console.log("叫~");
        }
    }
    class Dog extends Animal{
        
      run(){
        console.log(`${this.name}在跑`)
      }
      //重写
      sayHello(): void {
          console.log("汪汪")
      }
    }
    class Cat extends Animal{
       
    }
    
    const dog=new Dog("大黄",18);
    console.log(dog);
    dog.sayHello();
    dog.run();
    const cat=new Cat("咪咪",17);
    console.log(cat);
    cat.sayHello();

})();
```

super

```typescript
(function () {
  //在立即执行函数中，避免名称检查冲突
  class Animal {
    name: string;
    constructor(name: string) {
      this.name = name;
    }
    sayHello() {
      console.log("叫~");
    }
  }
  class Dog extends Animal {
    age: number;
    //重写
    constructor(name: string, age: number) {
      super(name);
      this.age = age;
    }
    sayHello(): void {
      super.sayHello();
    }
  }

  const dog = new Dog("大黄", 18);
  console.log(dog);
  dog.sayHello();
})();
```

#### 抽象类

```typescript
(function () {
  //在立即执行函数中，避免名称检查冲突
  /**
   * 抽象类
   * 不能被创建对象
   * java中的抽象类
   */
  abstract class Animal {
    name: string;
    constructor(name: string) {
      this.name = name;
    }
    abstract sayHello():void;
  }
  class Dog extends Animal {
    sayHello(): void {
      console.log("汪汪");     
    }
  }
})();
```

#### 接口

```typescript
(function () {
  /**
   * 描述一个对象的类型
   * 只能定义一个
   */
  type myType = {
    name: string;
    age: number;
  };
  /**
   * 接口,定义一个类结构
   * 可以重复定义
   * 所有属性不能有实际值
   */
  interface myInterface {
    name: string;
    age: number;
    sayHello(): void;
  }
  const obj: myType = {
    name: "s",
    age: 1,
  };
  const obj1: myInterface = {
    name: "s",
    age: 1,
    sayHello(): void {},
  };
  //类实现接口
  class Mycalss implements myInterface {
    name: string;
    age: number;
    constructor(name: string, age: number) {
      this.name = name;
      this.age = age;
    }
    sayHello(): void {
      throw new Error("Method not implemented.");
    }
  }
})();
```

#### 属性封装

```typescript
(function(){
    class Person{
        /**
         * 属性修饰符
         *  public
         *  protected
         *  private
         */
        public name:string;
        private _age:number;

        constructor(name:string,age:number){
            this._age=age;
            this.name=name;
        }

        // public getAge(){
        //     return this.age
        // }
        // ts简写,类似python装饰器
        get age(){
            return this._age;
        }
        // public setAge(value:number){
        //     if(value<0){
        //         value=0;
        //     }
        //     this._age=value;
        // }
        set age(value:number){
            if (value < 0) {
              value = 0;
            }
                    this._age=value;
        }

    }
    const per=new Person("孙悟空",500);
    // console.log(per.getAge());
    console.log(per.age);
    per.age=19;
    console.log(per.age);
})();
```

#### 泛型

```typescript
function fn<T>(a: T): T {
  return a;
}
function fn1<T, K>(a: T, b: K): T {
  return a;
}

//调用
let result = fn(10); //ts自动推断类型
let result1 = fn<string>("hello");
fn1<number, string>(123, "hello");

interface Inter {
  length: number;
}
//T extends Inter 表示泛型必须是Inter实现类（子类）
function fn2<T extends Inter>(a: T): number {
  return a.length;
}

class Mycalss<T> {
  constructor(public name: T) {}
}
```
