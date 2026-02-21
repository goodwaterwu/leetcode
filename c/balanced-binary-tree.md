[110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/description/)

```c
/* 110. Balanced Binary Tree - DFS with Height Check */

#define max(a, b) (((a) > (b)) ? (a) : (b))

/* 
 * Helper function to calculate height of tree.
 * Returns -1 immediately if subtree is unbalanced.
 */
int height(struct TreeNode *root) {
    if (!root)
        return 0;

    int left_h = height(root->left);
    int right_h = height(root->right);

    /* If any subtree is unbalanced or height difference > 1, return -1 */
    if (left_h == -1 || right_h == -1 || abs(left_h - right_h) > 1)
        return -1;

    /* Return height of current node */
    return max(left_h, right_h) + 1;
}

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* 
 * Main function to check if a binary tree is height-balanced.
 * Uses DFS and early termination via height() returning -1.
 */
bool isBalanced(struct TreeNode* root) {
    if (!root)
        return true;

    if (height(root) < 0)
        return false;

    return true;
}
```
