 #  __lvzu'daily tips__   #

>make progress everyday
---

## _2017/9/18_ ##
### 将Array中的重复元素删去 ###
```
var arr = [1,1,2,2,3,4,5,5,6]
arr = Array.from(new Set(arr))
```
### ES6编程风格问题 ###

####  1. boolean类型不能直接作为函数参数 ####
```
  var f = function(name,age,{options = false})
  f('lvzu',28,{options:true})
```
####  2. 类作为参数时 ####
```javascript
  var obj = {
    name:'lvzu',
    age:18,
  }

  //bad
  var f = function(obj){
    var name = obj.name
    var age = obj.age
  }
  f(obj)

  //good
  var f = function({name,age}){
  }
  f(obj)
```
#### 3. 关于set一个小坑 ####
```javascript
var map = new Map();

map.set(['a'], 555);
map.get(['a']) // undefined
```
#### 4. ES6模块化推荐用export
```javascript
//A.js
function getWindowH(){}
function setDate(){}
export{
  getWindowH,setDate
}

//B.js
import {getWindowH,setDate} from './A.js'
getWindowH()
```
#### 5.关于类的申明 ####
```javascript
  var set = [1,2,3]
  var myF = function () {
    console.log(1);
  }
  //bad
  var obj = {
    set:set,
    myF:myF
  }
  //good
  var obj = {
    set,
    myF,
  }
```
## _2017/9/19_ ##
### 微信小程序中的tarbar ###
```javascript
//在微信小程序中,若将某一页面设置在app.json的tarbar中，如

//app.json
"tabBar":{
    "borderStyle":"white",
    "selectedColor":"#294057",
    "list":[
      {
        "pagePath": "pages/index/index",
        "text": "首页",
        "iconPath":"./tabBar_img/index.png",
        "selectedIconPath":"./tabBar_img/index_on.png"
      },
    }
    
//则子页面中无法使用wx.navigateTo来进行跳转。而要使用
  wx.switchTab({
    url: '../index/index'
  })
```

### git中关于remote的操作 ###
```bash
  git remote -v #查看连接的远程仓库地址
  git remote remove origin #取消与远程仓库的绑定
  git remote add <地址> #新增远程仓库绑定
```
### Atom易忘记的快捷键 ###

```
  在深的目录下快速折叠 H
  选择括号中的内容    ctrl+alt+,
  打开关闭treeView   ctrl+|
  聚焦到treeView或者编辑器  alt+|
  在treeView中选中当前打开文件 shift + ctrl + \
```

## _2017/9/20_ ##
### 判断访问设备是手机还是pc ###
```javascript
    var sUserAgent = navigator.userAgent.toLowerCase();
    var bIsIpad = sUserAgent.match(/ipad/i) == "ipad";
    var bIsIphoneOs = sUserAgent.match(/iphone os/i) == "iphone os";
    var bIsMidp = sUserAgent.match(/midp/i) == "midp";
    var bIsUc7 = sUserAgent.match(/rv:1.2.3.4/i) == "rv:1.2.3.4";
    var bIsUc = sUserAgent.match(/ucweb/i) == "ucweb";
    var bIsAndroid = sUserAgent.match(/android/i) == "android";
    var bIsCE = sUserAgent.match(/windows ce/i) == "windows ce";
    var bIsWM = sUserAgent.match(/windows mobile/i) == "windows mobile";

    if (bIsIpad || bIsIphoneOs || bIsMidp || bIsUc7 || bIsUc || bIsAndroid || bIsCE || bIsWM) {
      console.log("phone");
    } else {
      console.log('pc');
    }

```

### \_\_proto\_\_ 与prototype ###

 基本概念:当我们访问一个对象的属性 时，如果这个对象内部不存在这个属性，那么他就会去__proto__里找这个属性，这个__proto__又会有自己的__proto__，于是就这样 一直找下去，也就是我们平时所说的原型链的概念.

如p.Say()
 若P没有Say这个function
 就从p.\_\_proto\_\_ 里找，即p.\_\_proto\_\_.Say()
 再找不到以此类推
 p.\_\_proto\_\_.\_\_proto\_\_.Say()


  <font color=#58B7FF size=4 face="黑体">example1:</font>
```javascript
	var Person = function () { }
	var p = new Person()
	p.__proto__ === Person.prototype //true
```
#### example1过程分析: 
上面这个例子得出一个概念，实例的__proto__等于类的prototype
  
  <font color=#58B7FF size=4 face="黑体">example2:</font>
```javascript
  var Person = function () {};
	Person.prototype.Say = function () {
	 alert("Person say");
	}
	var p = new Person();
	p.Say();
```
#### example2过程分析:  
  p.say()时p没有say，所以去p.__proto__里找,  
  p.__proto__ == Person.prototype  
  所以p.Say() --> p.__proto__.say -->   Person.prototype.Say()  

  <font color=#58B7FF size=4 face="黑体">example3:</font>
```javascript
	var Person = function () { };
		Person.prototype.Say = function () {
		alert("Person say");
	}
	Person.prototype.Salary = 50000;
 
	var Programmer = function () { };
	Programmer.prototype = new Person();
	Programmer.prototype.WriteCode = function () {
		alert("programmer writes code");
	};
 
	Programmer.prototype.Salary = 500;
 
	var p = new Programmer();
	p.Say();
	p.WriteCode();
	console.log(p.Salary);
```

#### example3过程分析:  
 Programmer.prototype = new Person();  
 根据上面的推论，得出  
  Programmer.prototype.\_\_proto\_\_ == Person.prototype  
  p = new Programmer()  
  p.\_\_proto\_\_ == Programmer.prototype    
  所以 p.Say()时，先找p自身没有Say方法，  
  然后找p.\_\_proto\_\_ 即 Programmer.prototype没有say方法  
  最后找p.\_\_proto\_\_.\_\_proto\_\_ 即   Programmer.prototype.\_\_proto\_\_ --> Person.prototype，发现/了Say方法  
  
### if的一种简略写法 ###
```javascript
var [a,b] = [1,2]
var myF = function(){
  console.log(1);
}

// 正常写法
if(a==b){
    myF()
}
// 简洁写法
a==b && myF()
```
这种简洁写法在上层已经有if的情况下比较好用,或在多种if判断下的赋值  
如这种需求: 如果金额等于0显示0个￥，大于0显示1个￥，大于5显示2个￥，大于10显示3个￥  
则可以简洁地写成:  
```javascript
var count = (money > 10 && 3) || (money > 5 && 2) || (money > 0 && 1) || 0
```
#### __补充__ ###
如果现在的需求是：  
金额等于0显示0个，金额等于5显示1个，金额等于10显示2个，等于15显示3个,其他显示0个  
则还有更简单的写法：
```javascript
var count={'0':0,'5':1,'10':2,'15':3}[money] || 0;
```


  

