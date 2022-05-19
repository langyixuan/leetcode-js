# 2、两数相加

## Add Two Numbers

**难度：中等😶**     **类型：链表-Linked List**

---

> 给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 `逆序` 的方式存储的，并且每个节点只能存储 一位 数字。
>
> 请你将两个数相加，并以相同形式返回一个表示和的链表。
>
> 你可以假设除了数字 0 之外，这两个数都不会以 0 开头。
>
> ```
> 输入：l1 = [2,4,3], l2 = [5,6,4]
> 输出：[7,0,8]
> 解释：342 + 465 = 807.
> ```



### 解题思路

<img src="C:\Users\郎艺璇\AppData\Roaming\Typora\typora-user-images\image-20220519180655293.png" alt="image-20220519180655293" style="zoom: 80%;" />

*对两数相加方法的可视化：*![[公式]](https://www.zhihu.com/equation?tex=342+%2B+465+%3D+807) *，每个节点都包含一个数字，并且数字按位逆序存储。*

就像你在纸上计算两个数字的和那样，我们首先从最低有效位也就是列表 ![[公式]](https://www.zhihu.com/equation?tex=+l1+) 和 ![[公式]](https://www.zhihu.com/equation?tex=+l2+) 的表头开始相加。由于每位数字都应当处于 ![[公式]](https://www.zhihu.com/equation?tex=+0%E2%80%A69+) 的范围内，我们计算两个数字的和时可能会出现 “溢出”。例如， ![[公式]](https://www.zhihu.com/equation?tex=5+%2B+7+%3D+12) 。在这种情况下，我们会将当前位的数值设置为 ![[公式]](https://www.zhihu.com/equation?tex=2) ，并将进位 ![[公式]](https://www.zhihu.com/equation?tex=+carry+%3D+1+) 带入下一次迭代。进位 ![[公式]](https://www.zhihu.com/equation?tex=+carry+) 必定是 ![[公式]](https://www.zhihu.com/equation?tex=0) 或 ![[公式]](https://www.zhihu.com/equation?tex=1) ，这是因为两个数字相加（考虑到进位）可能出现的最大和为 ![[公式]](https://www.zhihu.com/equation?tex=+9+%2B+9+%2B+1+%3D+19) 。

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    let resNode = new ListNode()  // 临时使用的 node 用来不停的增加链表节点
    let current = resNode  // current为指向当前节点的指针
    let carry = 0  // 用于保存相加的进位
	// l1和l2有一个非空就要据需循环计算
    while(l1 !== null || l2 !== null) {
        let sum = 0   // sum用于保存每次同为运算的计算结果
        if (l1 !== null) {  // l1非空时(没有遍历完)
            sum += l1.val
            l1 = l1.next
        }
        if (l2 !== null) {
            sum += l2.val
            l2 = l2.next
        }

        sum += carry  // 当前位运算加上进位
        current.next = new ListNode(sum % 10)  // 结果存入新节点，current指向新节点
        carry = Math.floor(sum / 10)  // 计算进位，往下传递 
        current = current.next  // current往下移动，直到指向最后一个节点
    }
    // 循环结束后，如果进位还是大于0，说明还需生成新的节点保存其最后的进位
    if (carry > 0) {
        current.next = new ListNode(carry)
    }
    return dummy.next
};
```

