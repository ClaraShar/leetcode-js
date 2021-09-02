# 179. 最大数

## 题目描述
给定一组非负整数 nums，重新排列每个数的顺序（每个数不可拆分）使之组成一个最大的整数。

注意：输出结果可能非常大，所以你需要返回一个字符串而不是整数。

示例：
```
输入：nums = [3,30,34,5,9]
输出："9534330"
``` 

## 解题思路
参考[题解](https://leetcode-cn.com/problems/largest-number/solution/li-yong-sortsi-xing-dai-ma-gao-ding-by-h-t9op/)
sort()排序会根据提供的排序函数返回数组；一般如果想要返回从小到大的排序，即：arr.sort((a, b) => a - b)
这个常用的规则意思是：如果前者a - 后者b大于零，a-b>0，就会返回true，true的时候sort函数会交换位置；直到从前到后变成从小到大。

本题其实要完成的就是一个类似的排序，即取a, b两个数，根据拼接之后的数判断：
以 [1, 12]为例，拼接之后比较'112'和'121'，即'ab'和'ba'，如果'ba'大的话，就交换顺序为[b, a]即[12, 1]；
最后根据顺序直接返回从前到后的拼接字符串[12, 1].join('')即可。
因此只需要改写排序的规则：如果拼接结果为ba更大，就交换位置。

## 代码
```
/**
 * @param {number[]} nums
 * @return {string}
 */
var largestNumber = function(nums) {
    nums.sort((a, b) => ('' + b + a) - ('' + a + b));
    return nums[0] == 0 ? '0' : nums.join('');
};
```

# 791. 自定义字符串排序

## 题目描述
字符串S和 T 只包含小写字符。在S中，所有字符只会出现一次。
S 已经根据某种规则进行了排序。我们要根据S中的字符顺序对T进行排序。更具体地说，如果S中x在y之前出现，那么返回的字符串中x也应出现在y之前。
返回任意一种符合条件的字符串T。

示例:
```
输入:
S = "cba"
T = "abcd"
输出: "cbad"
解释: 
S中出现了字符 "a", "b", "c", 所以 "a", "b", "c" 的顺序应该是 "c", "b", "a". 
由于 "d" 没有在S中出现, 它可以放在T的任意位置. "dcba", "cdba", "cbda" 都是合法的输出。
```

## 解题思路
参考[题解](https://leetcode-cn.com/problems/custom-sort-string/solution/js-by-feng-bu-hui-ting-xi-55/)
用map存字符和位置（S中index）的关系。map是一个长度为26的数组，按照S中元素出现的顺序存放进map，map[元素与‘a’的unicode差值] = index，其余没有在S中的字符index均为26，堆在map的后面 

## 代码
```
/**
 * @param {string} order
 * @param {string} s
 * @return {string}
 */
var customSortString = function(s, t) {
    const map = Array(26).fill(26)
    for(let i = 0; i < s.length; i++){
        map[s[i].charCodeAt() - 'a'.charCodeAt()] = i
    }
    var arr = t.split('').sort((a,b) => {
        const key1 = a.charCodeAt() - 'a'.charCodeAt()
        const key2 = b.charCodeAt() - 'a'.charCodeAt()
        return map[key1] - map[key2] //升序
    })
    return arr.join('')
};
```
