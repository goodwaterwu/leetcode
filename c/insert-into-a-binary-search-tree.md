[701. Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/description/)

```c
/* 701. Insert into a Binary Search Tree */

/* Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Insert a new value into the BST and return the root node */
struct TreeNode* insertIntoBST(struct TreeNode* root, int val) {
    struct TreeNode *tmp = root;
    struct TreeNode *node = (struct TreeNode *)malloc(sizeof(struct TreeNode));

    node->val = val;           /* Initialize the new node */
    node->left = NULL;
    node->right = NULL;

    if (!root)
        root = node;           /* If tree is empty, new node becomes the root */

    while (tmp) {
        if (tmp->val > val) {  /* Go to the left subtree */
            if (tmp->left) {
                tmp = tmp->left;
            } else {
                tmp->left = node; /* Insert as left child */
                break;
            }
        }
        else if (tmp->val < val) { /* Go to the right subtree */
            if (tmp->right) {
                tmp = tmp->right;
            } else {
                tmp->right = node; /* Insert as right child */
                break;
            }
        }
    }

    return root; /* Return the (possibly unchanged) root */
}
```
