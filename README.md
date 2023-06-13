# Leetcode-Python20

## 669.Trim a Binary Search Tree, 108.Convert Sorted Array to Binary Search Tree

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


## 108. Convert Sorted Array to Binary Search Tree
[leetcode](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)\
[video worth watching](https://www.bilibili.com/video/BV1uR4y1X7qL/?spm_id_from=333.788&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
Convert sorted array to binary search tree. This question is simpler. Firstly, we choose the middle number in the array as the middle node, and divide the array into left and right intervals, left and right boundries included in intervals division. Then use recursion to build left and right subtrees, and returned to the  root. 
```python
# ways 1: recursion
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def traversal(self, nums:List[int], left:int, right:int) -> TreeNode:
        if left > right:
            return None
        
        mid = left + (right - left)//2
        root = TreeNode(nums[mid])
        #build the left subtree and return to root, as root's left subtree
        root.left = self.traversal(nums, left, mid-1)  
        #build the right subtree and return to root, as root's right subtree 
        root.right = self.traversal(nums, mid + 1, right)
        return root

    def sortedArrayToBST(self, nums: List[int]) -> Optional[TreeNode]:
        root = self.traversal(nums, 0, len(nums) - 1)
        return root
```


## 538. Convert BST to Greater Tree
[leetcode](https://leetcode.com/problems/convert-bst-to-greater-tree/)\
Convert a binary search tree to an accumulating tree.在 求二叉搜索树的最小绝对差 和 众数 那两道题目 都讲过了 **two pointers**.\
Use inorder traversal, we can convert a binary search tree into an ordered array. Here we need to reverse it and use right-middle-left order traversal. Attention here, for the middle logic, we need to add the previous value to the current node, and update the previous pointer.\
Iteration is also another efficient way to solve this problem!
```python
# ways 1: recursion
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def convertBST(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        self.pre = 0  # 记录前一个节点的数值
        self.traversal(root)
        return root
    def traversal(self, cur):
        if cur is None:
            return        
        self.traversal(cur.right)
        cur.val += self.pre
        self.pre = cur.val
        self.traversal(cur.left)
```
```python
# ways 2: iteration
class Solution:
    def __init__(self):
        self.pre = 0  # 记录前一个节点的数值
    
    def traversal(self, root):
        stack = []
        cur = root
        while cur or stack:
            if cur:
                stack.append(cur)
                cur = cur.right  # 右
            else:
                cur = stack.pop()  # 中
                cur.val += self.pre
                self.pre = cur.val
                cur = cur.left  # 左
    
    def convertBST(self, root):
        self.pre = 0
        self.traversal(root)
        return root
```


## Summary of binary tree!!
[reading](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/%E4%BA%8C%E5%8F%89%E6%A0%91%E6%80%BB%E7%BB%93%E7%AF%87.md)
