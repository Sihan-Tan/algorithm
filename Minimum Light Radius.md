## Minimum Light Radius

You are given a list of integers `nums` representing coordinates of houses on a 1-dimensional line. You have `3` street lights that you can put anywhere on the coordinate line and a light at coordinate `x` lights up houses in `[x - r, x + r]`, inclusive. Return the smallest `r` required such that we can place the `3` lights and all the houses are lit up.

**Constraints**

- `n ≤ 100,000` where `n` is the length of `nums`

### Example 1



#### **Input**

```
nums = [3, 4, 5, 6]
```

#### **Output**

```
0.5
```

#### **Explanation**

If we place the lamps on `3.5`, `4.5` and `5.5` then with `r = 0.5` we can light up all `4` houses.

#### 思路

二分法

先排序，半径的长度为0~(最右-最左)，用这个直径作为mid，因为一共只有三栈灯，所以在确认两端的情况下，让中间的灯覆盖到剩余的中间区域

#### 代码

```typescript
class Solution {
    solve(nums: Array<number>): number {
        const len:number = nums.length;
        // 如果长度不满足，直接返回
        if (len <= 3) return 0;
        // 排序
        nums = nums.sort((a, b) => a - b);
        // 最左 和 最远的距离
        let left:number = 0, right:number = nums[len - 1] - nums[0];

        while(left < right) {
            let mid:number = left + Math.floor((right - left) / 2);
            // console.log(left, mid, right, this.isCover(nums, mid))
            if (this.isCover(nums, mid)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        console.log(left)
        return left / 2;
    }

    isCover(nums: Array<number>, dis: number) {
        let cur:number = nums[0], len:number = nums.length;
        let j:number = 0;
        for(let i:number = 0; i < 3; i ++) {
            cur += dis;
            while(j < len && nums[j] <= cur) {
                j++;
            }
            if (j == len) break;
            cur = nums[j]
        }
        return j == len;
    }
}
```

#### 复杂度分析

时间复杂度	$O()$

空间复杂度	$O(1)$

