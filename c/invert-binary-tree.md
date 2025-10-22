[226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/description/)

```c
/* 226. Invert Binary Tree */

/* Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Recursively invert the binary tree by swapping left and right children */
struct TreeNode* invertTree(struct TreeNode* root) {
    if (!root)
        return NULL; /* Base case: if node is NULL, return NULL */

    struct TreeNode *tmp = root->left; /* Temporarily store left child */

    root->left = root->right;  /* Swap left and right child */
    root->right = tmp;

    /* Recursively invert the subtrees */
    root->left = invertTree(root->left);
    root->right = invertTree(root->right);

    return root; /* Return the root of the inverted subtree */
}
```
