# 105. Construct Binary Tree from Preorder and Inorder Traversal

# Binary Tree Traversal

## preview

- **Preorder Traversal**
- **Inorder Traversal**
- **Postorder Traversal**

[](https://ithelp.ithome.com.tw/articles/10205571)

# Description:

## Given two integer arrays `preorder`
 and `inorder`
 where `preorder`
 is the preorder traversal of a binary tree and `inorder`
 is the inorder traversal of the same tree, construct and return *the binary tree*
.

**Example 1:**

![Untitled](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

**Example 2:**

```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```

# Code:

```cpp
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
    TreeNode* buildTree(vector<int>& pre, vector<int>& in) {
        if(pre.size()==0)return nullptr;
        TreeNode* root=new TreeNode(pre[0]);
        vector<int> l_pre;
        vector<int> r_pre;
        vector<int> l_in;
        vector<int> r_in;
        bool roott=false;
        for(int i=0;i<in.size();i++)
        {
            if(root->val==in[i]){
                roott=true;
                continue;
            }
            else{}
            if(roott){
                r_in.push_back(in[i]);
            }
            else{
                l_in.push_back(in[i]);
            }
        }
         if(pre.size()>1){
            l_pre.assign(pre.begin() + 1, pre.begin() + 1 + l_in.size());
            r_pre.assign(pre.begin() + 1+ l_in.size(), pre.end());
        }
            root->left = buildTree(l_pre, l_in);
            root->right = buildTree(r_pre, r_in);
        return root;
    }
};**
```

## inorder:

# **{[left Tree],[ROOT],[Right Tree]}**

# |                                |

     **{[left Tree],[ROOT],[Right Tree]}**           **{[left Tree],[ROOT],[Right Tree]}**

## then we use preorder size to judge whether its a nullptr.