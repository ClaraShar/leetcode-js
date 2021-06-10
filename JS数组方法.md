# reduce

## 语法
array.reduce(function(total, currentValue, currentIndex, arr), initialValue)

## 题目1
计算给定数组 arr 中所有元素的总和.

### 示例：
```
输入：[ 1, 2, 3, 4 ]
输出：10
``` 

### 代码
```
function sum(arr) {
    return arr.reduce(function(total, num){
        return total + num;
    });
}
```

## 题目2
在数组 arr 中，查找值与 item 相等的元素出现的所有位置

### 示例：
```
输入：['a','b','c','d','e','f','a','b','c'] 'a'
输出：[0, 6]
``` 

### 代码
```
function findAllOccurrences(arr, target) {
    return arr.reduce((res,curr,currIndex) => {
        if(curr == target){
            res.push(currIndex);
        }
        return res;
    }, [])
}
```

# 数组合并

## 题目描述
合并数组 arr1 和数组 arr2。**不要直接修改**数组 arr，结果返回新的数组。

### 1 字符串方式
```
function concat(arr1, arr2) {
    return (arr1 + ',' + arr2).split(",");
}
```


### 2 原生concat方式
```
function concat(arr1, arr2) {
    return arr1.concat(arr2);
}
```

### 3 扩展运算符
```
function concat(arr1, arr2) {
    return [...arr1, ...arr2];
}
```

# 数组方法小结
Splice会改变原数组;
slice([start,end))不改变原数组，只返回截取的元素。Concat、filter、map、flat不改变数组。