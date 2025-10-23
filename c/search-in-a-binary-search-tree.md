[700. Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/description/)

```c
/* 700. Search in a Binary Search Tree */

/* Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Recursively search for a node with the given value in a BST */
struct TreeNode* searchBST(struct TreeNode* root, int val) {
    struct TreeNode *node = NULL;

    if (!root)
        return NULL; /* Base case: node not found */

    if (root->val < val)
        node = searchBST(root->right, val); /* Search in right subtree */
    else if (root->val > val)
        node = searchBST(root->left, val);  /* Search in left subtree */
    else
        node = root; /* Found the target node */

    return node;
}
```
