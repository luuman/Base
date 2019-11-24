
# 数组合并

案例：将两个数据合并成一个

```
let a = [1, 2, 3]
let b = [4, 5, 6]
```

## concat
js的Array对象提供了一个叫concat()方法

```
let c = a.concat(b)
=> c = [1, 2, 3, 4, 5, 6]
```

## for循环
遍历其中一个数组，把该数组中的所有元素依次添加到另外一个数组中

```
for(var i in b) {
	a.push(b[i])
}
```


```
```

