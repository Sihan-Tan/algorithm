## 解法一
### 思路
1. 先转成数字，但是可能会越界，所以需要借助 BigInt 类型
2. 加1后再切成数组
### 代码
```javascript
var plusOne = function(digits) {
    let number = BigInt(digits.join(''))
    return (number+BigInt(1)).toString().split('')
};
```

### 复杂度分析

时间复杂度：O(1)

空间复杂度：O(1)







## 解法二

### 思路

1. 循环遍历，从低位开始

2. 如果有进位则继续遍历，如果没有进位，则直接退出

3. 当进位到最高位时，如果此时依旧有进位，那么此时的digits[0]必为0，则在数组开始的前面补1

   ```javascript
   var plusOne = function(digits) {
    let plus = 1;
    let len = digits.length - 1;
    for(let i = len; i >= 0;) {
        const tmp = digits[i] + 1;
        plus = tmp >= 10 ? 1 : 0
        digits[i] = plus ? tmp - 10 : tmp
        if (plus) {
            i --
        } else {
            return digits
        }
    }
    if (!digits[0]) {
        digits.unshift(1)
        return digits
    }
};
   ```

   ### 复杂度分析
   
   时间复杂度： O(N), 当全为9时
   
   空间复杂度：O(1)

