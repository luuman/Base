title: async 函数使用与原理
date: 2019-11-25 18:29:00
description: 
categories:
- JavaScript
tags:
- Promise
toc: true
author:
comments:
original:
permalink: 
---
　　**Promise**简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。 —— ECMAScript 6 入门 阮一峰
<!-- more -->

# 概况
ES2017标准引入async函数，异步操作更加简便。Generator函数的语法糖。

```javascript
const fs = require('fs')
const readFile = function (fileName) {
  return new Promise(function (resolve, reject) {
    fs.readFile(fileName, function(error, data) {
      if (error) return reject(error)
      resolve(data)
    })
  })
}
const gen = function* () {
	console.log('gen')
  const f1 = yield readFile('./etc/fstab.js')
  console.log('f1', f1)
  const f2 = yield readFile('./etc/shells.js')
  console.log('f2', f2)
}
const gens = gen()
gens.next()
// gens.next()
// gens.next()

const asyncReadFile = async function () {
  const f1 = await readFile('./etc/fstab.js')
  const f2 = await readFile('./etc/shells.js')
  console.log('async f', f1.toString())
  console.log('async f', f2.toString())
};
asyncReadFile()
```

# 基本用法
## 使用方法
1. async函数返回一个promise对象
1. 一旦执行到await就会等待返回值

```javascript
async function getName(){
	const symbol = await getSymbol(name)
	consot stockPrice = await getPrice(symbol)
	return stockPrice
}
getName().then((res) => {
	console.log(res)
})
```

## 多种使用形式
### 函数
```javascript
async function name() {}
```

### 密名函数
```javascript
const name = async function () {}
```

### 箭头函数
```javascript
const name = async () => {}
```

### 全局
```javascript
(async () => {})()
```

### Class
```javascript
class name{
  async name() {}
}
```
## 对象
```javascript
let name = {
	async name() => {}
}
```

```javascript
async function get() {

}
```

# 错误处理
1. await接收的错误异常会抛出错误

```javascript
const getError = function (fileName) {
  return new Promise(function (resolve, reject) {
    reject('error')
  })
}
getError().then(res => {}).catch(err => {
	console.log(err)
})
```

## tryCatch
```javascript
const getError = function (fileName) {
  return new Promise(function (resolve, reject) {
    reject('error')
  })
}
async function b() {
	try{
	  const res = await getError()
	  console.log(res)
	}catch(err) {
		console.log(err)
	}
}
b()
```

## 多个await
1. 多个await可以在一个try内，执行错误会抛出错误，但执行中止。

```javascript
const getError = function (fileName) {
  return new Promise(function (resolve, reject) {
    reject('error')
  })
}
async function b() {
	try{
		const num = await 1
	  console.log(num)
	  const res = await getError()
	}catch(err) {
		console.log(err)
	}
}
b()
```

## catch
```javascript
const getError = function (fileName) {
  return new Promise(function (resolve, reject) {
    reject('error')
  })
}
async function b() {
  const res = await getError()
  .catch(err => {
	  console.log(err)
  })
}
b()
```

## 多个catch
```javascript
const getError = function (fileName) {
  return new Promise(function (resolve, reject) {
    reject('error')
  })
}
async function b() {
  const res = await getError()
  .catch(err => {
	  console.log(err)
  })
	const num = await 1
  .catch(err => {
	  console.log(err)
  })
}
b()
```

# 并行
1. 默认执行为串行，执行await后才会执行吓一条。

## 串行
```javascript
const getError = function (fileName) {
  return new Promise(function (resolve, reject) {
    reject('error')
  })
}
async function b() {
  const res = await getError('may')
  const res = await getError('four')
}
b()
```

## 并行
```javascript
async function b() {
  const [may, four] = await Promise.all([getError('may'), getError('may')])
}
b()
```

## 并行
```javascript
async function b() {
	const may = getError('may')
	const four = getError('four')
  const res = await may
  const res = await four
}
b()
```

## 实践
```javascript
async function b() {
	let ArryName = ['name', 'four']
	const ArryPromise = []
	ArryName.map(item => ArryPromise.push(getError(item)))
}
```

# 原理
async 函数的实现原理，就是将 Generator 函数和自动执行器，包装在一个函数里。

```javascript
async function fn(args) {
  // ...
}

// 等同于

function fn(args) {
  return spawn(function* () {
    // ...
  });
}
```

```javascript
function spawn(genF) {
  return new Promise(function(resolve, reject) {
    const gen = genF();
    function step(nextF) {
      let next;
      try {
        next = nextF();
      } catch(e) {
        return reject(e);
      }
      if(next.done) {
        return resolve(next.value);
      }
      Promise.resolve(next.value).then(function(v) {
        step(function() { return gen.next(v); });
      }, function(e) {
        step(function() { return gen.throw(e); });
      });
    }
    step(function() { return gen.next(undefined); });
  });
}
```
与其他异步处理方法的比较
我们通过一个例子，来看 async 函数与 Promise、Generator 函数的比较。

假定某个 DOM 元素上面，部署了一系列的动画，前一个动画结束，才能开始后一个。如果当中有一个动画出错，就不再往下执行，返回上一个成功执行的动画的返回值。

首先是 Promise 的写法。

function chainAnimationsPromise(elem, animations) {

  // 变量ret用来保存上一个动画的返回值
  let ret = null;

  // 新建一个空的Promise
  let p = Promise.resolve();

  // 使用then方法，添加所有动画
  for(let anim of animations) {
    p = p.then(function(val) {
      ret = val;
      return anim(elem);
    });
  }

  // 返回一个部署了错误捕捉机制的Promise
  return p.catch(function(e) {
    /* 忽略错误，继续执行 */
  }).then(function() {
    return ret;
  });

}
虽然 Promise 的写法比回调函数的写法大大改进，但是一眼看上去，代码完全都是 Promise 的 API（then、catch等等），操作本身的语义反而不容易看出来。

接着是 Generator 函数的写法。

function chainAnimationsGenerator(elem, animations) {

  return spawn(function*() {
    let ret = null;
    try {
      for(let anim of animations) {
        ret = yield anim(elem);
      }
    } catch(e) {
      /* 忽略错误，继续执行 */
    }
    return ret;
  });

}
上面代码使用 Generator 函数遍历了每个动画，语义比 Promise 写法更清晰，用户定义的操作全部都出现在spawn函数的内部。这个写法的问题在于，必须有一个任务运行器，自动执行 Generator 函数，上面代码的spawn函数就是自动执行器，它返回一个 Promise 对象，而且必须保证yield语句后面的表达式，必须返回一个 Promise。

最后是 async 函数的写法。

async function chainAnimationsAsync(elem, animations) {
  let ret = null;
  try {
    for(let anim of animations) {
      ret = await anim(elem);
    }
  } catch(e) {
    /* 忽略错误，继续执行 */
  }
  return ret;
}
可以看到 Async 函数的实现最简洁，最符合语义，几乎没有语义不相关的代码。它将 Generator 写法中的自动执行器，改在语言层面提供，不暴露给用户，因此代码量最少。如果使用 Generator 写法，自动执行器需要用户自己提供。

```javascript
```

```javascript
```


注意：
1. await命令必须在async，否则报错。
1. await可以接非Promise
1. 

[async](http://es6.ruanyifeng.com/?search=async&x=0&y=0#docs/async)
[如何逃离 async/await 困境](https://www.infoq.cn/article/await-hell)
[理解 JavaScript 的 async/await](https://segmentfault.com/a/1190000007535316)
[如何避开 async/await 地狱](https://juejin.im/post/5b9db6925188255c3b7d78cb)
[精读《async/await 是把双刃剑》](https://juejin.im/post/5aefbb046fb9a07ab508cf25)
[前端er，你真的会用 async 吗？](https://juejin.im/post/5c0397186fb9a049b5068e54)
[嘿，不要给 async 函数写那么多 try/catch 了](https://juejin.im/post/5d25b39bf265da1bb67a4176)
[深入理解 ES7 的 async/await]()
