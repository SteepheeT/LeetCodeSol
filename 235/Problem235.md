# Problem235 - Lowest Common Ancestor of a Binary Search Tree - Medium
Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST.

According to *the definition of LCA on Wikipedia*[^1]: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a **node to be a descendant of itself**).”

 

**Example 1:**

![Example1](235e1.png)

```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
Explanation: The LCA of nodes 2 and 8 is 6.
```

**Example 2:**

![Example2](235e2.png)

```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
Output: 2
Explanation: The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.
```

**Example 3:**
```
Input: root = [2,1], p = 2, q = 1
Output: 2
```

**Constraints:**

- The number of nodes in the tree is in the range `[2, 105]`.
- `-10^9 <= Node.val <= 10^9`
- All `Node.val` are **unique**.
- `p != q`
- `p` and `q` will exist in the BST.
---
## Solution - C++ 
### 51 ms, 23.3 mb
- This problem can be solved by **recursively access the branch of the BST**, since we already knew the two node, the next problem is to decide which branch(s) contains our node.
- This method works because of the following reason:
- 1. If the two `nodes` are located at different sides of the `root` node, then no matter the *`position`* and the *`depth`*, their common ancestor will always be the `root` node.
- 2. If one of the two `nodes` is the curret `root` node, the no matter where the rest node is, their common ancestor will be the current `root` node.
- 3. If the two `nodes` are located at the same sides of the `root` node, either left or right, we can go long with this branch to check the possible common ancestor node.
- 3. Each time we arrived a new `root` node, we will decide if the current `root` node could be the common ancestor following reason ***1 & 2***.
```
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    bool seperate = p->val > q->val?
                    p->val >= root->val && q->val <= root->val:
                    p->val <= root->val && q->val >= root->val;
    if(seperate){
        return root;
    }
    TreeNode* anc = nullptr;
    bool left = p->val < root->val;
    if(left){
        anc = traverse(root->left, p, q);
    }
    else{
        anc = traverse(root->right, p, q);
    }
    return anc;
}

TreeNode* traverse(TreeNode* root, TreeNode* p, TreeNode* q){
    bool seperate = p->val > q->val?
                    p->val >= root->val && q->val <= root->val:
                    p->val <= root->val && q->val >= root->val;
    if(seperate){
        return root;
    }
    bool left = p->val < root->val;
    if(left)
        return traverse(root->left, p, q);
    else
        return traverse(root->right, p, q);
}
```

### 32 ms, 23.4 mb
- This is the improvement / simply version of the previous solution, t**he main principles solving this problem are the same**, but shortened the code.
- We only use one function to decide which branch to visit, or return the current `root` node.
```
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if(p->val < root->val && q->val < root->val){
        return lowestCommonAncestor(root->left, p, q);
    }
    else if(p->val > root->val && q->val > root->val){
        return lowestCommonAncestor(root->right, p, q);
    }
    else
        return root;
}
```

---
[^1]: https://en.wikipedia.org/wiki/Lowest_common_ancestor