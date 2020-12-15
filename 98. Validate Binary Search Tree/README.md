# 98. Validate Binary Search Tree

Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:

    The left subtree of a node contains only nodes with keys less than the node's key.
    The right subtree of a node contains only nodes with keys greater than the node's key.
    Both the left and right subtrees must also be binary search trees.

注意二叉搜索树的定义，The left subtree 和 The right subtree，是左子树和右子树 ，不是左节点和右节点。做比较判断的时候要注意
	
## Example

Input: root = [2,1,3]
Output: true

Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.

## solution

1.中序遍历二叉搜索树，所有元素添加到数组中，然后判断数据是否是升序

备注：前序遍历、中序遍历、后序遍历

```
class Solution {
public:
    vector<int> vec;
    
    bool isValidBST(TreeNode* root) {
         //遍历二叉树 转成 vector
        convert(root);
        
        //遍历vector，判断是升序就可以
        for(int index=1; index<vec.size(); index++)
        {
            if(vec[index] <= vec[index-1])
            {
                return false;
            }
        }
        return true;
    }
    
   
    void convert(TreeNode* root)
    {
        if(root == NULL)
        {
            return;
        }
        
        convert(root->left);
        vec.push_back(root->val);
        convert(root->right);
        
    }
};
```