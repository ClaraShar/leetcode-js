# 剑指 Offer 07. 重建二叉树

## 题目描述
输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。

假设输入的前序遍历和中序遍历的结果中都不含重复的数字。


示例 1：
![avatar](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)
```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```
示例 2：
```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```

## 解题思路
跟二叉树有关都是递归思想。
前序是先遍历根结点（中左右），中序是左中右，所以前序的第一个元素就是树根，在中序中以树根元素划分左右子树。


## 代码
```
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {number[]} preorder
 * @param {number[]} inorder
 * @return {TreeNode}
 */
var buildTree = function(preorder, inorder) {
    if(!preorder.length || !inorder.length) return null;
    let root = preorder[0]
    let rootIndex = inorder.indexOf(root)
    let node = new TreeNode(root)
    node.left = buildTree(preorder.slice(1,rootIndex+1),inorder.slice(0,rootIndex))
    node.right = buildTree(preorder.slice(rootIndex+1),inorder.slice(rootIndex+1))
    return node;
};
```