# Problem 98 - Validate Binary Search Tree - Medium
Given the `root` of a binary tree, *determine if it is a valid binary search tree (BST)*.

A **valid BST** is defined as follows:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.
 

**Example 1:**

![Example1](98e1.jpg)
```
Input: root = [2,1,3]
Output: true
```
**Example 2:**

![Example2](98e2.jpg)
```
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `-2^31 <= Node.val <= 2^31 - 1`
---
## Solution - C++

### 13 ms, 21.7 mb
- We assign a extra minimum long value to help us judge whether the tree is valid.
- Since the minimum value of integer is included according to *Constraints* section, we need a even smaller number.
- Using In-order traversal to check the BST, and once we hit the left-most node, the comparison begins.

- If the current Node is:
- - ***Null*** - then we return true, as if the root node is null, the the "tree" would still be considered as valid BST.
- - ***Not Null*** - then we compare if current node's value **is larger than** `max_val`, we update `max_val`.

- This method works for the following reason:
- - At the left-most node of the tree, since our initial value of `max_val` is the minimum value of *`long`*, which is smaller than the minimum of *`int`*, we will update `max_val` to the left-most node's value. 
- - Using *`LONG_MIN`* instead of *`INT_MIN`* is to prevent the left-most node's value is exactly *`INT_MIN`*, causing return `false` instantly.
- - When comparing right children: before call and visit current root's right child, `max_val` will be updated to current node's value. Current node's value is expected to **be smaller than** its right child's.

```
long long max_val = LONG_MIN;
bool isValidBST(TreeNode* root) {
    return traverse(root);
}

bool traverse(TreeNode* root){
    if(!root)
        return true;

    bool l_valid = traverse(root->left);

    if(root->val > max_val)
        max_val = root->val;
    else
        return false;

    bool r_valid = traverse(root->right);

    return l_valid && r_valid;
}
```

### 9 ms, 21.5 mb
- Improvemnt of the last version using two pointers instead of a LONG_MIN value parameter.
- We directly compare two node's value while traversal.

```
TreeNode* pre = nullptr;
bool isValidBST(TreeNode* root) {
    return traverse(root);
}

bool traverse(TreeNode* root){
    if(!root)
        return true;
        
    bool l_valid = traverse(root->left);

    if(pre && pre->val >= root->val)
        return false;
    pre = root;

    bool r_valid = traverse(root->right);

    return l_valid && r_valid;
}
```