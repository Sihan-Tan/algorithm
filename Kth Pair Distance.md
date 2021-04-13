## Kth Pair Distance

Given a list of integers `nums` and an integer `k`, return the `k`-th (0-indexed) smallest `abs(x - y)` for every pair of elements `(x, y)` in `nums`. Note that `(x, y)` and `(y, x)` are considered the same pair.

**Constraints**

- `n ≤ 100,000` where `n` is the length of `nums`

### Example 1

#### **Input**

```
nums = [1, 5, 3, 2]
k = 3
```

#### **Output**

```
2
```

#### **Explanation**

Here are all the pair distances:

- `abs(1 - 5) = 4`
- `abs(1 - 3) = 2`
- `abs(1 - 2) = 1`
- `abs(5 - 3) = 2`
- `abs(5 - 2) = 3`
- `abs(3 - 2) = 1`

Sorted in ascending order we have `[1, 1, 2, 2, 3, 4]`.

#### 思路

二分可能的答案，答案是在[0,max(nums)-min(nums)]之间。然后对于二分中的mid，我们需要知道这个mid在pair_distance的rank是多少，这样我们就需要对一个sort好的nums去做能力检测。

#### 代码

```typescript
class Solution {
    solve(nums: Array<number>, k: number): number {
        nums = nums.sort((a, b) => a - b);
        const len:number = nums.length;
        let l:number = 0, r:number = nums[len - 1] - nums[0];

        while (l < r) {
            let mid = l + r >> 1;
            let cnt = this.check(nums, mid);
            if (cnt >= k + 1) r = mid;
            else l = mid + 1;
        }
        return l
    }

    check(nums: Array<number>, mid: number) {
        let len:number = nums.length, left:number = 0;
        let cnt:number = 0;
        for (let i:number = 0; i < len; ++i) {
            while (nums[i] - nums[left] > mid) left++;
            cnt += i - left;
        }
        return cnt;
    }
}
```

#### 复杂度分析

时间复杂度	$O(nlogN)$

空间复杂度	$O(1)$

