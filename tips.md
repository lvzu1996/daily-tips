# **lvzu'daily tips**

## >make progress everyday

## _2017/9/18_

### 将Array中的重复元素删去

```
var arr = [1,1,2,2,3,4,5,5,6]
arr = Array.from(new Set(arr))
```

### ES6编程风格问题

#### 1\. boolean类型不能直接作为函数参数

```
  var f = function(name,age,{options = false})
  f('lvzu',28,{options:true})
```

#### 2\. 类作为参数时

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

#### 3\. 关于set一个小坑

```javascript
var map = new Map();

map.set(['a'], 555);
map.get(['a']) // undefined
```

#### 4\. ES6模块化推荐用export

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

#### 5.关于类的申明

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

## _2017/9/19_

### 微信小程序中的tarbar

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

### git中关于remote的操作

```bash
  git remote -v #查看连接的远程仓库地址
  git remote remove origin #取消与远程仓库的绑定
  git remote add <地址> #新增远程仓库绑定
```

### Atom易忘记的快捷键

```
  在深的目录下快速折叠 H
  选择括号中的内容    ctrl+alt+,
  打开关闭treeView   ctrl+|
  聚焦到treeView或者编辑器  alt+|
  在treeView中选中当前打开文件 shift + ctrl + \
```

## _2017/9/20_

### 判断访问设备是手机还是pc

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

### __proto__ 与prototype

基本概念:当我们访问一个对象的属性 时，如果这个对象内部不存在这个属性，那么他就会去**proto**里找这个属性，这个**proto**又会有自己的**proto**，于是就这样 一直找下去，也就是我们平时所说的原型链的概念.

如p.Say() 若P没有Say这个function 就从p.__proto__ 里找，即p.__proto__.Say() 再找不到以此类推 p.__proto__.__proto__.Say()

<font color="#58B7FF" size="4" face="黑体">example1:</font>

```javascript
    var Person = function () { }
    var p = new Person()
    p.__proto__ === Person.prototype //true
```

#### example1过程分析:

上面这个例子得出一个概念，实例的**proto**等于类的prototype

<font color="#58B7FF" size="4" face="黑体">example2:</font>

```javascript
  var Person = function () {};
    Person.prototype.Say = function () {
     alert("Person say");
    }
    var p = new Person();
    p.Say();
```

#### example2过程分析:

p.say()时p没有say，所以去p.**proto**里找,<br>
p.\_\_proto\_\_ == Person.prototype<br>
所以p.Say() --> p.\_\_proto\_\_.say --> Person.prototype.Say()

<font color="#58B7FF" size="4" face="黑体">example3:</font>

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

Programmer.prototype = new Person();<br>
根据上面的推论，得出<br>
Programmer.prototype.__proto__ == Person.prototype<br>
p = new Programmer()<br>
p.__proto__ == Programmer.prototype<br>
所以 p.Say()时，先找p自身没有Say方法，<br>
然后找p.__proto__ 即 Programmer.prototype没有say方法<br>
最后找p.__proto__.__proto__ 即 Programmer.prototype.__proto__ --> Person.prototype，发现/了Say方法

### if的一种简略写法

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

这种简洁写法在上层已经有if的情况下比较好用,或在多种if判断下的赋值<br>
如这种需求: 如果金额等于0显示0个￥，大于0显示1个￥，大于5显示2个￥，大于10显示3个￥<br>
则可以简洁地写成:

```javascript
var count = (money > 10 && 3) || (money > 5 && 2) || (money > 0 && 1) || 0
```

#### **补充**

如果现在的需求是：<br>
金额等于0显示0个，金额等于5显示1个，金额等于10显示2个，等于15显示3个,其他显示0个<br>
则还有更简单的写法：

```javascript
var count={'0':0,'5':1,'10':2,'15':3}[money] || 0;
```

### 设置了DOCTYPE之后发现的一个小问题

今天登录自己网站的main页面，发现原本会随着滚轮变化的导航栏背景色没反应了<br>
后来对着git提交记录和main.vue相关部分来了一通乱找，也没发现问题所在，<br>
百度了半天，最后终于发现了问题所在，如下

```javascript
//没有设置DOCTYPE时
//监听滚轮 设置header-fa的background-color
window.onscroll = function () {
  let opacity = document.body.scrollTop/212
  $('#header-fa').css('background-color',`rgba(32, 160, 255,${opacity})`)
}


// 页面指定了DOCTYPE时，使用document.documentElement。
window.onscroll = function () {
  let opacity = document.documentElement.scrollTop/212
  $('#header-fa').css('background-color',`rgba(32, 160, 255,${opacity})`)
}
```

### 传入一个obj，传出一个加上了公共参数的obj
```javascript
GetReqParam: function(data){
      var t = this
      return Object.assign({}, {
          _id: t.G.userInfo._id
      }, (data||{}))
  },
```

## _2017/9/21_

### 身份证号规则&或可用于正则匹配
```javascript
//输入身份证号前17位，计算最后一位并输出完整身份证号码
function calc(str)
{
	var coeff = [7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2,1];
	var suffix = ['1','0','x','9','8','7','6','5','4','3','2'];
	var sum = 0;
	for(var i=0;i<17;i++)
		sum += coeff[i] * parseInt(str.charCodeAt(i)-48);
	sum %= 11;
	str = str.substr(0,17) + suffix[sum];
	return str;
}
calc('33010220090101493')
```

### 接收一个音频文件并转化为拥有多种分析工具的对象
```html

<html lang="en">
<head>
  <title>Document</title>
</head>
<body>
  <div class="container">
    <input type="file" id="file"  />
    <script>
    var fileBox = document.getElementById('file');
    fileBox.onchange = function () {
        //获取选择文件的数组
        var fileList = fileBox.files;
        for (var i = 0; i < fileList.length; i++) {
            var file = fileList[i];
            var reader = new FileReader();
            reader.readAsArrayBuffer(file);
            reader.onload = function () {
              console.info(reader.result); //中文字符串
              var audioCtx = new AudioContext()
              audioCtx.decodeAudioData(reader.result).then(function(res){
                console.log(res)
              })
            };
        }
    }
    
  </script>
</div>
</body>
</html>
```
## _2017/9/22_

### 浅谈ArrayBuffer和各种视图类 ###

####先讲ArrayBuffer  
javascript 中用数组来储存长度较小的数据，而因为数组的一些缺陷导致  
array用于储存较大长度的数据时的性能不忍直视，于是乎，arraybuffer就这样出现了  
ArrayBuffer对象被用来表示一个通用的，固定长度的二进制数据缓冲区，__不能被直接读写__  
上面这个性质也决定了他的构造函数只有一个，那就是  
 ```javascript
    var arrBuffer = new ArrayBuffer (length)
 ```
 其二，既然不能读写，那我们要如何去使用呢，这就要引出各种buffer类型化的数组了
####TypedArray
光说无益，先全部写出来，你肯定见过一些
```javascript
Int8Array(); 
Uint8Array(); 
Uint8ClampedArray();
Int16Array(); 
Uint16Array();
Int32Array(); 
Uint32Array(); 
Float32Array(); 
Float64Array();
```
庞大的TypedArray家族，先只写两个比较常用的Uint8Array和Uint32Array(其他没踩过坑)

Uint8Array是一个数组，而且数组中储存的是不带符号的8位整数，  
也就是0~2^8-1 所以可以写 Uint8Array[index]=(0~255) 但是写256就不行了
同理，Uint32Array保存了32位不带符号整数,也就是Uint32Array[index] 可以等于(0~2^32-1)


####代码
```javascript
var arrayBuffer = new ArrayBuffer(16)

	var u8a = new Uint8Array(arrayBuffer)
  console.log(u8a);//Uint8Array [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ] 
  for(let i in u8a){
		u8a[i] = 1
	}
  var arrBufView = new Uint8Array(arrayBuffer)
	console.log(arrBufView);//Uint8Array [ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 ]
```
分析：先创建了一个ArrayBuffer对象，长度为16，  也就是现在这个arrayBuffer对象指向了一块16个字节的内存，  16个字节也就是16x8 = 128位2进制数。  这块内存最大可以保存0-2^16-1 这范围内的数

在第二行代码中申明了一个Uint8Array类型的对象，并且指向我们上面创建的ArrayBuffer实例，打印结果为//Uint8Array [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ] ，因为ArrayBuffer对象初始化默认置为0

后面的代码中做了一个循环，将u8a中的元素全部置为1,打印发现原来arrBuf对应的内存也做了改变，这就是如何写ArrayBuffer对象的方式

```javascript
	var ab = new ArrayBuffer(16)

	var u32a = new Uint32Array(ab)
	u32a[0] = Math.pow(2,16*8/4)-1
	console.log(u32a);

	var u8a = new Uint8Array(ab)
	console.log(u8a);
  //Uint32Array [ 4294967295, 0, 0, 0 ]
  //Uint8Array [ 255, 255, 255, 255, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ]
```
分析：Uint32Array保存的是32位整数，也就是2^32，原数据是2^(16\*8),所以u32a[index]对应的就是2^(32\*index)大小的数

### 一段语音数据化的js代码，接收音频文件arraybuffer，输出一个元素为Uint8Array的数组 ###
input:ArrayBuffer  
output:array[Uint8Array,Uint8Array...]  

代码地址
 [语音分析模块](https://github.com/lvzu1996/my-utils/blob/master/analyse.js/)



