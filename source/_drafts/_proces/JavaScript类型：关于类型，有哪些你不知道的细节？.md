类型
	1. Undefined
	1. Null
	1. Boolean
	1. String
	1. Number
	1. Symbol
	1. Object

## 为什么有的编程规范要求用 void 0 代替 undefined？

### Backbone.js

``` javascript
if (callback !== void 0 && 'context' in opts && opts.context === void 0) opts.context = callback;
```
在ES5之前，window下的undefined是可以被重写的，于是导致了某些极端情况下使用undefined会出现一定的差错。

所以，用void 0是为了防止undefined被重写而出现判断不准确的情况。

> 注： ES5之后的标准中，规定了全局变量下的undefined值为只读，不可改写的，但是局部变量中依然可以对之进行改写。The void operator evaluates the given expression and then returns undefined.