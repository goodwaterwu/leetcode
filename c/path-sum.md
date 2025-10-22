[112. Path Sum](https://leetcode.com/problems/path-sum/description/)

```c
/* 112. Path Sum */

/* Definition for a binary tree node */
/* struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Determine if the tree has a root-to-leaf path such that the sum of the node values equals targetSum */
bool hasPathSum(struct TreeNode* root, int targetSum) {
    if (!root)
        return false; /* Base case: empty node, no path exists */

    /* If it's a leaf node and the value equals the remaining targetSum, path found */
    if (!root->left && !root->right && root->val == targetSum)
        return true;

    /* Recursively check left and right subtrees with updated targetSum */
    bool left = hasPathSum(root->left, targetSum - root->val);
    bool right = hasPathSum(root->right, targetSum - root->val);

    /* Return true if any path satisfies the condition */
    return (left || right);
}
```
