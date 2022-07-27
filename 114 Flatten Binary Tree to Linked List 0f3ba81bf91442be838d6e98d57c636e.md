# 114. Flatten Binary Tree to Linked List

Given the `root` of a binary tree, flatten the tree into a "linked list":

- The "linked list" should use the same `TreeNode` class where the `right` child pointer points to the next node in the list and the `left` child pointer is always `null`.
- The "linked list" should be in the same order as a **[pre-order traversal](https://en.wikipedia.org/wiki/Tree_traversal#Pre-order,_NLR)** of the binary tree.

**Example 1:**

![https://assets.leetcode.com/uploads/2021/01/14/flaten.jpg](https://assets.leetcode.com/uploads/2021/01/14/flaten.jpg)

```
Input: root = [1,2,5,3,4,null,6]
Output: [1,null,2,null,3,null,4,null,5,null,6]

```

**Example 2:**

```
Input: root = []
Output: []

```

**Example 3:**

```
Input: root = [0]
Output: [0]

```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 2000]`.
- `100 <= Node.val <= 100`

### Code:

```csharp
**/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    void flatten(TreeNode* root) {
        if(root == nullptr) return;
        vector<int> rec;
        traverse(root->left,rec);
        traverse(root->right,rec);
        for(int i=0;i<rec.size();i++) 
        {
            TreeNode* node = new TreeNode(rec[i]);
            root->right=node;
            root->left=nullptr;
            root=root->right;
        }
        return;
    }
    void traverse(TreeNode* root,vector<int>& rec)
    {
        if(root == nullptr) return;
        rec.push_back(root->val);
        traverse(root->left,rec);
        traverse(root->right,rec);
    }
};**
```

### Solution:

**use vector to  record every node (pre-order).**

**put all the nodes of vector to the right and let left be nullptr.**