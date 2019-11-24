# 初级算法
## 数组
### 从排序数组中删除重复项

``` javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
  let keys = {}
  let sum = []
  let n = 0
  nums.forEach((item, index) => {
    if (!keys[item]) {
      keys[item] = true
    } else {
      sum.push(index)
    }
  })
  sum.forEach((item) => {
    n++
    nums.splice(item - n, 1)
  })
  return nums.length
};
```