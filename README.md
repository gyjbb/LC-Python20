# Leetcode-Python20

## 669. Trim a Binary Search Tree

June 12, 2023  4h

Congratulations!\
This is the twentieth day for leetcode python study. Today we will learn more about the Binary Tree!\
The challenges today are about ~~need to delete later~~.


## 669. Trim a Binary Search Tree
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0669.%E4%BF%AE%E5%89%AA%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.md)\
[video worth watching](https://www.bilibili.com/video/BV17P41177ud/?spm_id_from=pageDriver&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
[leetcode](https://leetcode.com/problems/trim-a-binary-search-tree/)\
This question is harder than inserting and deleting from a binary search tree.\
The results in the termination conditions will be returned to the upper level. The upper level's logic follows the termination conditions.
```python
# ways 1: recursion
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def trimBST(self, root: Optional[TreeNode], low: int, high: int) -> Optional[TreeNode]:
        if root is None:
            return None
        if root.val < low:
            # look for the nodes on the right side of deleted node and between [low, high] 
            right = self.trimBST(root.right, low, high)
            return right
        if root.val > high:
            # look for the nodes on the left side of deleted node and between [low, high] 
            left = self.trimBST(root.left, low, high)
            return left
        root.left = self.trimBST(root.left, low, high)  # root.left connects to the qualified left subtree
        root.right = self.trimBST(root.right, low, high)  # root.right connects to the qualified right subtree
        return root
```


## 108.

将有序数组转换为二叉搜索树  
本题就简单一些，可以尝试先自己做做。






## 538.

把二叉搜索树转换为累加树  
本题也不难，在 求二叉搜索树的最小绝对差 和 众数 那两道题目 都讲过了 双指针法，思路是一样的。






## Summary of binary tree!!
