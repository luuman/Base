```javascript
const url = 'https://www.baidu.com/s?wd=javascript&rsv_spt=1&show=true'

function queryURL(url) {
	let reg = /([^&?=]+)=([^&=]+)/g
	let obj = {}
	url.replace(reg, () => {
		obj[arguments[1], arguments[2]]
	})
	return obj
}
queryURL(url)
```