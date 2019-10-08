Array.prototype.fakeMap = function (fn, context) {
	if (typeof fn != 'function') throw new TypeError(`${fn} is not a function`) 
	let arrg = this
	let sum = []
	for (let i = 0; i < arrg.length; i++) {
		sum.push(fn.call(context, arr[i], i, arr))
	}
	return sum
}

var arr = ['x', 'y', 'z']
arr.fakeMap(item => item++)
console.log(arr)


call 、bind 、 apply


Function.prototype.fakecall = function (context) {
	let self = context

}




```javascript
Array.prototype.fakeMap = function (fn, context) {
	if (typeof fn != 'function') throw new TypeError(`${fn} is not a function`)
	let self = this
	let arr = []
	for (let i = 0; i < self.length; i++) {
		arr.push(fn.call(context, self[i], i, self ))
	}
	return arr
}
var arr = ['x', 'y', 'z']

console.log(arr.fakeMap(item => item++))
```

```javascript
Array.prototype.fakeFilter = function (fn, context) {
	if (typeof fn != 'function') throw new TypeError(`${fn} is not a function`)
	let self = this
	let arr = []
	for (let i = 0; i < self.length; i++) {
		if (fn.call(context, self[i], i, self)) arr.push(self[i])
	}
	return arr
}
var arr = ['x', 'y', 'z']

console.log(arr.fakeFilter(item => item == 'x'))
```

## reduce
```javascript
Array.prototype.fakeReduce = function (fn, initialValue) {
	if (typeof fn != 'function') throw new TypeError(`${fn} is not a function`)
	let self = this
	let sum = initialValue || self[0]
	let start = initialValue ? 0 : 1
	for (let i = start; i < self.length; i++) {
		sum = fn(sum, self[i], i, self)
	}
	return sum
}
var arr = [1, 2, 3]

console.log(arr.fakeReduce((prev, cur) => prev + cur))
```