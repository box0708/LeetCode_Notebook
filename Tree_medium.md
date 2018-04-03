## 95. **Unique Binary Search Trees II**

> Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1...n.

Note: the way of combining different trees.

```cpp
class Solution {
public:
    vector<TreeNode*> generateTrees(int n) {
        return helper(1, n);
    }
    
    vector<TreeNode*> helper(int start, int end) {
        vector<TreeNode*> A;
        if (start > end) return A;
        else{
            for (int value=start; value<=end; value++){
                vector<TreeNode*> left_list = helper(start, value-1);
                vector<TreeNode*> right_list = helper(value+1, end);
                
                if (left_list.size()==0 && right_list.size()==0){
                    TreeNode* root = new TreeNode(value);
                    A.push_back(root);
                }
                
                else if (left_list.size() == 0){
                    for (int right=0; right<right_list.size(); right++){
                        TreeNode* root = new TreeNode(value);
                        root->right = right_list[right];
                        A.push_back(root);
                    }
                }
                
                else if (right_list.size() == 0){
                    for (int left=0; left<left_list.size(); left++){
                        TreeNode* root = new TreeNode(value);
                        root->left = left_list[left];
                        A.push_back(root);
                    }
                }
                
                else{
                    for (int left=0; left<left_list.size(); left++){
                        for (int right=0; right<right_list.size(); right++){
                            TreeNode* root = new TreeNode(value);
                            root->left = left_list[left];
                            root->right = right_list[right];
                            A.push_back(root);
                        }
                    }
                }
            }
        }
        return A;
    }
};
```
