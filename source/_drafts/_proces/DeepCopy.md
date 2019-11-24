## 变量类型
对值类型进行复制操作会对值进行一份拷贝，而对引用类型赋值，则会进行地址的拷贝，最终两个变量指向同一份数据。深拷贝和浅拷贝都是针对的引用类型。
### 基本类型
字符串（string）、数值（number）、布尔值（boolean）、undefined、null、[symbol]("http://es6.ruanyifeng.com/#docs/symbol")
### 引用类型
对象（Object）、数组（Array）、函数（Function）

浅拷贝只复制指向某个对象的指针，而不复制对象本身，新旧对象还是共享同一块内存。但深拷贝会另外创造一个一模一样的对象，新对象跟原对象不共享内存，修改新对象不会改到原对象。

## 浅拷贝
### 引用类型导致赋值
数组赋值对象，浅拷贝导致数据联动
```JavaScript
var Arry = [
]

let obj = {
    name:'name',
    job:'job'
}
Arry.push(obj)
obj.name = 'a'
console.log(Arry)
// [{name: "a", job: "job"}]
console.log(obj)
// {name: "a", job: "job"}
```

### 引用类型导致的问题
数组倒置需拷贝至新数组才能不影响原数组
Array.reverse() 方法将数组中元素的位置颠倒，并返回该数组。该方法会改变原数组。
```JavaScript
var arrA = [1, 2, 3, 4]
var arrB = arrA.reverse()
console.log(arrA)
// [4, 3, 2, 1]
console.log(arrB)
// [4, 3, 2, 1]
```

```JavaScript
var arrB = arrA = {
  a: 1,
  b: 2
}
arrB.b = 3
console.log(arrA)
// {a: 1, b: 3}
console.log(arrB)
// {a: 1, b: 3}
```

### 数组
```JavaScript
var arrA = [1, 2, 3, 4]
var arrB = arrA.slice()
// 浅拷贝
// 数组倒置需拷贝才能不影响原数组
arrB.reverse()
console.log(arrA)
// [1, 2, 3, 4]
console.log(arrB)
// [4, 3, 2, 1]
arrB[1] = 0
console.log(arrA)
// [1, 2, 3, 4]
console.log(arrB)
// [4, 0, 2, 1]
```

### 对象浅拷贝
```JavaScript
var obj = [
  {
    name:'melin1',
    job:'111'
  },
  {
    name:'melin2',
    job:'222'
  },
  {
    name:'melin3',
    job:'333'
  }
]
var copy = obj.slice(0)
console.log(obj, copy)
copy[1].name = 'tom'
console.log(obj[1].name)
//tom
console.log(copy[1].name)
//tom
```
slice可看作浅拷贝，因为如果obj有引用类型的元素，slice仅仅是复制了元素的地址。

如果obj所有值都是非引用类型，那么obj.slice(0)与深浅拷贝没有差别；
如果obj有引用类型的元素的话，obj.slice(0)仅仅是复制了元素的地址，obj.slice(0)可看作浅拷贝。

### ES6 数组浅拷贝

```JavaScript
var obj = [
  {
    name:'melin1',
    job:'111'
  },
  {
    name:'melin2',
    job:'222'
  },
  {
    name:'melin3',
    job:'333'
  }
]
var copy = [...obj]
console.log(obj, copy)
copy[1].name = 'tom'
console.log(obj[1].name)
//tom
console.log(copy[1].name)
//tom
```

```JavaScript
const arrA = [1, 2, 3, 4]
const arrB = [...arrA]
arrB.reverse()
console.log(arrA)
// [1, 2, 3, 4]
console.log(arrB)
// [4, 3, 2, 1]
```
### 数组深拷贝
```JavaScript
var arrB = arrA = [1, 2, 3, 4]
arrB = arrB.reverse()
console.log(arrA)
// [4, 3, 2, 1]
console.log(arrB)
// [4, 3, 2, 1]
```

## 深拷贝

### 递归拷贝

### 深拷贝实现--元素的类型判断
为了每个对象都能通过 Object.prototype.toString() 来检测，需要以 Function.prototype.call() 或者 Function.prototype.apply() 的形式来调用，传递要检查的对象作为第一个参数，称为thisArg。
```JavaScript
function getType(obj) {
  //tostring会返回对应不同的标签的构造函数
  var toString = Object.prototype.toString
  var map = {
    '[object Boolean]'  : 'boolean', 
    '[object Number]'   : 'number', 
    '[object String]'   : 'string', 
    '[object Function]' : 'function', 
    '[object Array]'    : 'array', 
    '[object Date]'     : 'date', 
    '[object RegExp]'   : 'regExp', 
    '[object Undefined]': 'undefined',
    '[object Null]'     : 'null', 
    '[object Object]'   : 'object'
  }
  if(obj instanceof Element) {
    return 'element'
  }
  return map[toString.call(obj)]
}
let obj = {
  name:'melin1',
  job:'111'
}
let arrA = [1, 2, 3, 4]
console.log(getType(obj))
// object
console.log(getType(arrA))
// array
```

### 递归拷贝

```JavaScript
function getType(obj) {
  //tostring会返回对应不同的标签的构造函数
  let toString = Object.prototype.toString
  let map = {
    '[object Boolean]'  : 'boolean', 
    '[object Number]'   : 'number', 
    '[object String]'   : 'string', 
    '[object Function]' : 'function', 
    '[object Array]'    : 'array', 
    '[object Date]'     : 'date', 
    '[object RegExp]'   : 'regExp', 
    '[object Undefined]': 'undefined',
    '[object Null]'     : 'null', 
    '[object Object]'   : 'object'
  }
  if (obj instanceof Element) return 'element'
  return map[toString.call(obj)]
}
function deepClone(data){
  let Type = getType(data)
  let obj
  if (Type === 'object') {
    obj = {}
  } else if (Type === 'array') {
    obj = []
  } else {
    return data
  }
  if (Type === 'array') {
    data.forEach(item => {
      obj.push(deepClone(item))
    })
  } else if (Type === 'object') {
    for (let key in data) {
      obj[key] = deepClone(data[key])
    }
  }
  return obj
}
let obj = [{
  name:'melin1',
  job:'111'
}]
let objs = [{
  name:'melin1',
  job:'111'
}]
var copy = obj.slice(0)
console.log(deepClone(obj), copy)
// [ { name:'melin1', job:'111' } ]
// [ { name:'tom', job:'111' } ]

obj[0].name = 'tom'
let arrA = [1, 2, 3, 4]
console.log(deepClone(arrA), copy)
// [1, 2, 3, 4]
// [ { name:'tom', job:'111' } ]

let obj = {         
    reg : /^asd$/,
    fun: function(){},
    syb:Symbol('foo'),
    asd:'asd'
}; 
let cp1 = deepClone(obj)
console.log(cp);
// {reg: /^asd$/, fun: ƒ, syb: Symbol(foo), asd: "asd"}
```

### 树的广度优先遍历
> 缺点：

1. 不能复制正则
```JavaScript
// 这里为了阅读方便，只深拷贝对象，关于数组的判断参照上面的例子
function deepClone(data){
  var obj = {}
  var originQueue = [data]
  var copyQueue = [obj]
  //以下两个队列用来保存复制过程中访问过的对象，以此来避免对象环的问题（对象的某个属性值是对象本身）
  var visitQueue = []
  var copyVisitQueue = []
  while(originQueue.length > 0){
    var _data = originQueue.shift()
    var _obj = copyQueue.shift()
    visitQueue.push(_data)
    copyVisitQueue.push(_obj)
    for(var key in _data){
      var _value = _data[key]
      if(typeof _value !== 'object'){
        _obj[key] = _value
      } else {
        //使用indexOf可以发现数组中是否存在相同的对象(实现indexOf的难点就在于对象比较)
        var index = visitQueue.indexOf(_value)
        if(index >= 0){
          // 出现环的情况不需要再取出遍历
          _obj[key] = copyVisitQueue[index]
        } else {
          originQueue.push(_value)
          _obj[key] = {}
          copyQueue.push(_obj[key])
        }
      }
    }
  }
  return obj
}
let obj = {         
    reg : /^asd$/,
    fun: function(){},
    syb:Symbol('foo'),
    asd:'asd'
}; 
let cp1 = deepClone(obj)
console.log(cp);
// {reg: {}, fun: ƒ, syb: Symbol(foo), asd: "asd"}
```

### JSON解析反解析
JSON.parse(JSON.stringify(obj)) 深拷贝对象还有另一个解决方法，在对象中不含有函数的时候，使用JSON解析反解析就可以得到一个深拷贝对象

> 缺点：

1. 不能复制function、正则、Symbol
1. 循环引用报错
1. 相同的引用会被重复复制

```JavaScript
var obj = [
  {
    name:'melin1',
    job:'111'
  },
  {
    name:'melin2',
    job:'222'
  },
  {
    name:'melin3',
    job:'333'
  }
]
var copy = JSON.parse(JSON.stringify(obj))
copy[1].name = 'tom'
console.log(obj[1].name)
//melin2
console.log(copy[1].name)
//tom

var obj = {
    name:'melin3',
    job:'333'
  }
var copy = JSON.parse(JSON.stringify(obj))
copy.name = 'tom'
console.log(obj)
// {name: "melin3", job: "333"}
console.log(copy)
// {name: "tom", job: "333"}
```

#### 应用：vue 父子组件传递数据深拷贝
场景：父组件props向子组件传递数据，若为引用类型（数组or对象），子组件改变该数据时会影响父组件数据，不想改变时可以深拷贝该数据再做操作。
```JavaScript
computed: {
  data: function () {
    var obj={}
    obj=JSON.parse(JSON.stringify(this.templateData))
    //this.templateData是父组件传递的对象
    return obj
  }
}
```

### lodash
另外一个很热门的函数库lodash，也有提供_.cloneDeep用来做 Deep Copy。

```JavaScript
var _ = require('lodash');
var obj1 = {
    a: 1,
    b: { f: { g: 1 } },
    c: [1, 2, 3]
};
var obj2 = _.cloneDeep(obj1);
console.log(obj1.b.f === obj2.b.f);
// false
```

### jquery
jquery 有提供一个$.extend可以用来做 Deep Copy。
```JavaScript
var $ = require('jquery');
var obj1 = {
    a: 1,
    b: { f: { g: 1 } },
    c: [1, 2, 3]
};
var obj2 = $.extend(true, {}, obj1);
console.log(obj1.b.f === obj2.b.f);
// false
```


```JavaScript
```