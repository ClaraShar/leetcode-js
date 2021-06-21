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

# arguments

## 原理
arguments是一个类数组对象，包含调用函数时传入的所有参数。这个对象只有以function关键字定义函数（想对于箭头函数）时才会有。

## 题目
函数 useArguments 可以接收 1 个及以上的参数。请实现函数 useArguments，返回所有调用参数相加后的结果。本题的测试参数全部为 Number 类型，不需考虑参数转换。

### 示例
```
输入：1, 2, 3, 4
输出：10
```

### 代码
```
function useArguments() {
    //解构
    var arr = [...arguments];
    return arr.reduce(function(total, curNum){
        return total + curNum;
    })
}
```

# apply & call & bind

## 原理
call和apply都是为了解决改变 this 的指向。通过指定this值来调用函数。改变上下文。
call 和 apply传参的方式不同。除了第一个参数（this值）外，call 可以接收一个参数列表(逐个列出)，apply 只接受一个参数数组。
bind返回一个函数。

## 题目1
实现函数 callIt，调用之后满足如下条件
1、返回的结果为调用 fn 之后的结果
2、fn 的调用参数为 callIt 的第一个参数之后的全部参数

### 代码
```
function callIt(fn) {
    var arr = [...arguments];
    return fn.apply(this, arr.slice(1));
}
```

## 题目2
封装函数 f，使 f 的 this 指向指定的对象

### 代码1
```
function bindThis(f, oTarget) {
    return function(){
        return f.apply(oTarget, [...arguments]);
    }
}
```

### 代码2
```
function bindThis(f, oTarget) {
    eturn  f.bind(oTarget);
}
```

### 题解
由于题目要求封装一个函数，所以如果用apply和call方法的话要在方法外包装一个function，但是使用bind方法则可以不封装，因为bind可以返回一个函数。

## 题目3
实现函数 partialUsingArguments，调用之后满足如下条件：
1、返回一个函数 result
2、调用 result 之后，返回的结果与调用函数 fn 的结果一致
3、fn 的调用参数为 partialUsingArguments 的第一个参数之后的全部参数以及 result 的调用参数

### 代码
```
function partialUsingArguments(fn) {
    var arr1 = [...arguments].slice(1);
    return function result(){//1
        var arr2 = [...arguments];
        return fn(...arr1,...arr2);//2、3
    }
}
```

### 题解
这道题可以看题说话。也可以用biind、apply等方法(暂时还不会)。

# 闭包问题

## 描述
闭包是指一个函数引用了另一个函数作用域中的变量，闭包问题可以用bind。

## 题目
实现函数 makeClosures，调用之后满足如下条件：
1、返回一个函数数组 result，长度与 arr 相同
2、运行 result 中第 i 个函数，即 result[i]()，结果与 fn(arr[i]) 相同

## 代码
```
function makeClosures(arr, fn) {
    let result=[];
    for(let i=0;i<arr.length;i++){
        result[i]=fn.bind(this,arr[i]);
    }
    return result;
}
```