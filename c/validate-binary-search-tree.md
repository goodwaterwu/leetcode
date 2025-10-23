[98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/description/)

```c
/* 98. Validate Binary Search Tree */

/* Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Helper function to validate if a binary tree satisfies BST properties within given bounds */
bool isValid(struct TreeNode *root, long long int min, long long int max) {
    if (!root)
        return true; /* Base case: empty tree is valid */

    if (root->val <= min || root->val >= max)
        return false; /* Node violates the BST property */

    /* Recursively validate left and right subtrees with updated bounds */
    return (isValid(root->left, min, root->val) && 
            isValid(root->right, root->val, max));
}

/* Check if the entire binary tree is a valid BST */
bool isValidBST(struct TreeNode* root) {
    long long int min = LLONG_MIN; /* Smallest possible value */
    long long int max = LLONG_MAX; /* Largest possible value */

    return isValid(root, min, max); /* Start recursive validation */
}
```
