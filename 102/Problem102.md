# Problem 102 - Binary Tree Level Order Traversal - Medium
Given the `root` of a binary tree, return *the level order traversal of its nodes' values*. (i.e., from left to right, level by level).

 

**Example 1:**

![Example1](102e1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
```

**Example 2:**
```
Input: root = [1]
Output: [[1]]
```
**Example 3:**
```
Input: root = []
Output: []
```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 2000]`.
- `-1000 <= Node.val <= 1000`

---
## Solution - C++

### 8 ms, 12.5 mb
```
vector<vector<int>> levelOrder(TreeNode* root) {
    vector<vector<int>> ans;
    if(!root)
        return ans;
    
    queue<TreeNode*> que;
    que.push(root);

    while(!que.empty()){
        int length = que.size();
        vector<int> temp;
        for(int i=0; i<length; i++){
            TreeNode* current = que.front();
            que.pop();
            temp.push_back(current->val);
            
            if(current->left)
                que.push(current->left);
            if(current->right)
                que.push(current->right);
        }
        ans.push_back(temp);
    }
    return ans;
}
```