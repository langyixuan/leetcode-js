# 11-盛水最多的容器

## Container With Most Water 

**难度：中等 😶**       **类型：数组-Array**

> 给定一个长度为 n 的整数数组 height 。有 n 条垂线，第 i 条线的两个端点是 (i, 0) 和 (i, height[i]) 。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。返回容器可以储存的最大水量。
>
> ![image-20220517222749542](C:\Users\郎艺璇\AppData\Roaming\Typora\typora-user-images\image-20220517222749542.png)
>
> 输入：[1,8,6,2,5,4,8,3,7]
> 输出：49 
> 解释：图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。



### 解题思路

第一反应，暴力破解，把所有的可能算一遍，时间复杂度是`O(n2)`。这肯定是不行的，于是我们需要找找规律。

我们现在有两个指针，分别指向第一根和最后一根。

假设 第一根高度是 H1，最后一根高度是Hn，H1大于Hn，所以他们围出来的面积是多少呢？`Hn*（n-1）`。

现在我们要让其中一根指针向里移动，还要面积有可能上升。我们思考，面积取决于两根柱子的距离和两根柱子中最短的一根。现在，我们向里移动，两个指针指向的柱子的相对距离变短了，我们为了面积上升，只能选择让两根柱子中较短的那一根长度较长，于是，我们要移动指向较短的柱子的那一个指针。

循环上述操作，两个指针相遇时结束循环，完成遍历。

于是，经过分析和双指针的引入，时间复杂度`从O(n2)`变成了`O(n)`

```javascript
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function(height) {
    let i = 0
    let j = height.length - 1
    let maxArea = 0
    while(i < j) {
        const temp = (j - i)*Math.min(height[i], height[j])
        maxArea = Math.max(maxArea, temp)
        if (height[i] > height[j]) {
            j -= 1
        } else {
            i += 1
        }
    }
    return maxArea
};
```

