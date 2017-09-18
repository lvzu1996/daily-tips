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
