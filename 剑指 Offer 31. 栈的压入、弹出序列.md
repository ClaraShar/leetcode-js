# 剑指 Offer 31. 栈的压入、弹出序列

## 题目描述
输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。

示例 1：
```
输入：pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
输出：true
解释：我们可以按以下顺序执行：
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
```

示例 2：
```
输入：pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
输出：false
解释：1 不能在 2 之前弹出。
```

## 解题思路
栈的操作可以首先考虑到辅助栈，借助辅助栈来实现一些操作:
1. 借助一个辅助栈，模拟一遍弹出的操作
2. 每插入一个元素到辅助栈中，判断是否可进行弹出操作
3. 直到弹出全部元素，如果能够弹出，说明成功，否则失败。

## 代码
```
/**
 * @param {number[]} pushed
 * @param {number[]} popped
 * @return {boolean}
 */
var validateStackSequences = function(pushed, popped) {
    let stack = []
    let j = 0
    for(let i = 0; i < pushed.length; i++) {
        stack.push(pushed[i])
        // 针对每个pushed元素，判断能否弹出的条件
        while(stack.length > 0 && popped[j] === stack[stack.length-1]) {
            stack.pop()
            j++ //弹出之后popped指针后移一位
        }
    }
    return stack.length > 0 ? false : true
};
```