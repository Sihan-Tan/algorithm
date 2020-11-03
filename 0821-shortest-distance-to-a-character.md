## 思路

1. 先遍历一遍，将目标字符串标记，并存入
2. 再次遍历，找到距离较小的值

## 代码

```javascript
var shortestToChar = function(S, C) {
  const arr = [], indexArr = []
  const len = S.length
  for(let i = 0; i < len; i ++) {
      if (S[i] === C) {
          arr[i] = 0
          indexArr.push(i)
      }
  }
  for(let i = 0, j = 0; i < len; i++) {
      if (arr[i] === 0 && j + 1 < indexArr.length) {
          j++
          continue
      }
      if (indexArr[j - 1] !== undefined) {
          arr[i] = Math.min(Math.abs(indexArr[j] - i), i - indexArr[j - 1])
      } else {
          arr[i] = Math.abs(indexArr[j] - i)
      }
  }
  return arr
};
```

## 复杂度分析

时间复杂度：O(N)

空间复杂度:   O(N)