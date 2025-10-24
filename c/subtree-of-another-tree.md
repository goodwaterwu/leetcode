[572. Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/description/)

```c
/* 572. Subtree of Another Tree */
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Helper function to check if two binary trees are identical */
bool isSameTree(struct TreeNode *root1, struct TreeNode *root2) {
    /* Both nodes are NULL → trees are identical */
    if (!root1 && !root2)
        return true;

    /* One node is NULL and the other is not → trees differ */
    if (!root1 || !root2)
        return false;

    /* Node values differ → trees differ */
    if (root1->val != root2->val)
        return false;

    /* Recursively check left and right subtrees */
    return (isSameTree(root1->left, root2->left) && isSameTree(root1->right, root2->right));
}

/* Main function to check if subRoot is a subtree of root */
bool isSubtree(struct TreeNode* root, struct TreeNode* subRoot) {
    /* Both trees empty → subRoot is subtree */
    if (!root && !subRoot)
        return true;

    /* One tree empty and the other not → not a subtree */
    if (!root || !subRoot)
        return false;

    /* If current nodes match, return true */
    if (isSameTree(root, subRoot))
        return true;

    /* Otherwise, recursively check left and right subtrees */
    return (isSubtree(root->left, subRoot) || isSubtree(root->right, subRoot));
}
```
