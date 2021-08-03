# 剑指 Offer II 004. 只出现一次的数字 

## 题目描述
给你一个整数数组 nums ，除某个元素仅出现 一次 外，其余每个元素都恰出现 三次 。请你找出并返回那个只出现了一次的元素。

示例：
```
输入：nums = [0,1,0,1,0,1,100]
输出：100
```

## 解题思路
不难，注意边界

## 代码
```
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function(nums) {
    nums.sort()
    let only;
    for(let i = 0; i < nums.length; i++){
        only = nums[i];
        if(nums[i+1] == only) i += 2
        else break
    }
    return only;
};
```