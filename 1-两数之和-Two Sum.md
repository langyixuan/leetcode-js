# 1、两数之和

## Two Sum

**难度：简单😎**       **类型：数组-Array**

---

> 给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出和为目标值 target 的那两个整数，并返回它们的数组下标。
> 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。
> 你可以按任意顺序返回答案。
>
> 示例 1：
> 输入：nums = [2,7,11,15], target = 9
> 输出：[0,1]
> 解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 



### 方法一：双指针循环

💡 思路: 第一个数从前往后循环，第二个数从后往前循环，找出符合要求的两个数字

```javascript
var twoSum = function(nums, target) {
    let i, j;
    let length = nums.length
    for(i = 0; i < length; i++) {
        for(j = length - 1; j > i; j--) {
            if (nums[i] + nums[j] === target) {
                return [i, j]
            }
        }
    }
};
```



### 方法二：Map

💡 思路: 创建一个map结构(可以将key存储为任意类型), for循环遍历nums数组, 用target减去nums[i]的值从而计算哪个数字能跟当前的nums[i]相加得到target,  在map中检测是否有这个数，如果有则返回结果，没有将nums[i]当作key，将i当作value放入map中。

```javascript
var twoSum = function(nums, target) {
    const map = new Map()
    for (let i = 0; i < nums.length; i++) {
        let temp = target - nums[i]
        if (map.has(temp)) {
            return [map.get(temp), i]
        } else {
            map.set(nums[i], i)
        }
    }
    return []
};
```

 
