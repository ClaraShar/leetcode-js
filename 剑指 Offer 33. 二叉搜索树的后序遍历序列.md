# 剑指 Offer 33. 二叉搜索树的后序遍历序列

## 题目描述
输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 true，否则返回 false。假设输入的数组的任意两个数字都互不相同。

参考以下这颗二叉搜索树：
```
     5
    / \
   2   6
  / \
 1   3
```

示例 1：
```
输入: [1,6,3,2,5]
输出: false
```
示例 2：
```
输入: [1,3,2,6,5]
输出: true
```

## 解题思路
牢记这句话：*跟二叉树有关都是递归思想。*
前序是先遍历根结点（中左右），中序是左中右，后序是左右中。所以后序最后一个元素就是树根。
还有一个关键：*在题目没有重复数字的前提下，二叉搜索树的左子树均小于根节点，右子树均大于根节点。*
所以只需要递归判断右子树是否均大于根节点。


## 代码
```
/**
 * @param {number[]} postorder
 * @return {boolean}
 */
var verifyPostorder = function(postorder) {
    var len = postorder.length;
    if(postorder.length < 2) return true;
    var root = postorder[len - 1]
    //划分左右子树
    var i = 0;
    for( ;i < len - 1; i++){
        if(postorder[i] > root) break;
    }
    // 判断右子树中的元素是否都大于 root，此处用到 every (数组 API，数组的每个元素都返回 true 则整体返回 true)
    var result = postorder.slice(i, len - 1).every(x => x > root)
    if(result){
        return(verifyPostorder(postorder.slice(0,i)) && verifyPostorder(postorder.slice(i,len - 1)))
    }else{
        return false;
    }
};
```