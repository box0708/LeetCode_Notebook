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

## 101. Symmetric Tree

Recursive

```cpp
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (root == NULL){
            return NULL;
        }
        
        TreeNode* temp = root->left;
        root->left = root->right;
        root->right = temp;
        
        root->left = invertTree(root->left);
        root->right = invertTree(root->right);
        
        return root;
    }
};
```

## 437. Path Sum III


> You are given a binary tree in which each node contains an integer value.
> 
> Find the number of paths that sum to a given value.
> 
> The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).
> 
> The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

```cpp
class Solution {
public:
    int pathSum(TreeNode* root, int sum) {
        if (root == NULL){
            return 0;
        }
        
        return helper(root, sum) + pathSum(root->left, sum) + pathSum(root->right, sum);
    }
    
    int helper(TreeNode* root, int sum) {
        int res = 0;
        if (root == NULL){
            return 0;
        }
        
        if (sum == root->val){
            res++;
        }
        
        res = res + helper(root->left, sum - root->val) + helper(root->right, sum - root->val);
        
        return res;
    }
};
```
