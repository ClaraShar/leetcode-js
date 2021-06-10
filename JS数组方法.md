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

# 柯里化

## 原理
指的是将能够接收多个参数的函数转化为接收单一参数的函数。

## 题目1
实现函数 functionFunction，调用之后满足如下条件：
1、返回值为一个函数 f
2、调用返回的函数 f，返回值为按照调用顺序的参数拼接，拼接字符为英文逗号加一个空格，即 ', '
3、所有函数的参数数量为 1，且均为 String 类型

### 示例：
```
输入：functionFunction('Hello')('world')
输出：Hello, world
```

### 代码
```
function functionFunction(str) {
    return function(str1){
        return str = str + ", " + str1;
    }
}
```

## 题目2
已知 fn 为一个预定义函数，实现函数 curryIt

### 示例：
```
输入： var fn = function (a, b, c) {return a + b + c}; curryIt(fn)(1)(2)(3);
输出： 6
```

### 代码
```
function curryIt(fn) {
    return function a(xa){
        return function b(xb){
            return function c(xc){
                return fn.call(this,xa,xb,xc);//call通过指定this值来调用函数，这里调用fn。与上一题类似，只是上一题直接在这里写了函数体
            };
        };
    };
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
