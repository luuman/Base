
forEach
	arr.forEach()
		声明式
		特点
			不支持return
	for(let key in arr)
		编程式
		特点
			key为String类型
			返回值包括数组的私有属性
	for(let val of arr)
		编程式
		特点
			支持return
			arr为数组，不能为对象
	for(let i = 0; i < arr.length; i++)
		编程式
		特点
			支持return
			arr为数组，不能为对象


