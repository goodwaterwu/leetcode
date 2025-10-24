[543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/description/)

```c
/* 543. Diameter of Binary Tree */
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Helper function to calculate the height of the tree and update the diameter */
int treeHeight(struct TreeNode *root, int *diameter) {
    int left = 0;
    int right = 0;

    if (!root)
        return 0; /* Base case: empty subtree has height 0 */

    /* Recursively compute the heights of left and right subtrees */
    left = treeHeight(root->left, diameter);
    right = treeHeight(root->right, diameter);

    /* Update the diameter if the current path is longer */
    if (left + right > *diameter)
        *diameter = left + right;

    /* Return the height of the current subtree */
    return ((left > right) ? left + 1 : right + 1);
}

/* Main function to find the diameter of a binary tree */
int diameterOfBinaryTree(struct TreeNode* root) {
    int diameter = 0;

    /* Compute the diameter through recursive height traversal */
    treeHeight(root, &diameter);

    return diameter;
}
```
