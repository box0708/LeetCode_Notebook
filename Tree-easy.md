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

## 501. Find Mode in Binary Search Tree

> Given a binary search tree (BST) with duplicates, find all the mode(s) (the most frequently occurred element) in the given BST.
> 
> Assume a BST is defined as follows:
> 
> > The left subtree of a node contains only nodes with keys less than or equal to the node's key.
> >
> > The right subtree of a node contains only nodes with keys greater than or equal to the node's key.
> >
> > Both the left and right subtrees must also be binary search trees.

```cpp
class Solution {
public:
    vector<int> findMode(TreeNode* root) {
        vector<int> res;
        if (root == NULL){
            return res;
        }
        
        stack<TreeNode*> node_stack;
        TreeNode* node = root;
        TreeNode* last = NULL;
        int count=1, maximum=0;
        
        while (node != NULL || node_stack.empty() != true){
            while (node != NULL){
                node_stack.push(node);
                node = node->left;
            }
            
            node = node_stack.top();
            node_stack.pop();
            
            if (last){
                count = (node->val == last->val) ? count + 1 : 1;
            }
            
            if (count >= maximum) {
                if (count > maximum) {
                    res.clear();
                }
                res.push_back(node->val);
                maximum = count;
            }
            
            last = node;
            node = node->right;
        }
        return res;
    }
};
```
## 538. Convert BST to Greater Tree

> Given a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus sum of all keys greater than the original key in BST.

1. The reverse of the inorder traverse of a BST is what we need.

2. Record a ```sum```, the sum of all the numbers which is bigger than the current number.

```cpp
class Solution {
public:
    TreeNode* convertBST(TreeNode* root) {
        if (!root){
            return NULL;
        }
        
        int sum=0;
        helper(root, sum);
        return root;
    }
    
    void helper(TreeNode* root, int& sum){
        if (!root){
            return;
        }
        
        helper(root->right, sum);
        root->val = root->val + sum;
        sum = root->val;
        helper(root->left, sum);
    }
};
```
