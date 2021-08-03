# 剑指 Offer 64. 求1+2+…+n

## 题目描述
求 1+2+...+n ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

示例：
```
输入: n = 3
输出: 6
```

## 解题思路
一行代码。考虑到公式为：（n+1）* n / 2，（n+1）* 2 = n^2+n，用Math.pow()做平方，右移一位即除以二。
看题解还有用递归的，return n && n + sumNums(--n)

## 代码
```
/**
 * @param {number} n
 * @return {number}
 */
var sumNums = function(n) {
    return ( Math.pow(n, 2) + n ) >> 1;
};
```