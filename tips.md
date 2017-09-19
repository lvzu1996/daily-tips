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

