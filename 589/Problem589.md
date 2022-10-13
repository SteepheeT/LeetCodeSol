# Problem 589 - N-ary Tree Preorder Traversal - Easy
Given the `root` of an n-ary tree, return the *preorder traversal of its nodes' values*.

Nary-Tree input serialization is represented in their level order traversal. Each group of children is separated by the null value (See examples)

 

**Example 1:**

[<img src="589e1.png" width="400"/>](589e1.png)
```
Input: root = [1,null,3,2,4,null,5,6]
Output: [1,3,5,6,2,4]
```
**Example 2:**

[<img src="589e2.png" width="400"/>](589e2.png)
```
Input: root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
Output: [1,2,3,6,7,11,14,4,8,12,5,9,13,10]
```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 104]`.
- `0 <= Node.val <= 104`
- The height of the n-ary tree is less than or equal to `1000`.
 

**Follow up:** Recursive solution is trivial, could you do it iteratively?

---
## Solution - C++

### 50 ms, 11.1 mb
```
vector<int> preorder(Node* root) {
    vector<int> ans;
    helper(root, ans);
    return ans;
}

void helper(Node* root, vector<int>& ans){
    if(!root)
        return ;
    ans.push_back(root->val);
    for(auto& child: root->children)
        helper(child, ans);
        
}
```