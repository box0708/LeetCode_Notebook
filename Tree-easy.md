## 101. Symmetric Tree

> Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).
> 
> For example, this binary tree ```[1,2,2,3,4,4,3]``` is symmetric
> 
> But the following ```[1,2,2,null,3,null,3]``` is not:

```cpp
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if (root == NULL){
            return true;
        }
        
        else{
            return check(root->left, root->right);
        }
    }
    
    bool check(TreeNode* n1, TreeNode* n2){
        if (n1 == NULL && n2 == NULL){
            return true;
        }
        
        if (n1 == NULL || n2 == NULL){
            return false;
        }
        
        if (n1->val != n2->val){
            return false;
        }
        
        return (n1->val == n2->val && check(n1->left, n2->right) && check(n1->right, n2->left));
    }
};
```
