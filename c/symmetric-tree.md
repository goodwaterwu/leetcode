[101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/description/)

```c
/* 101. Symmetric Tree */

/* Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Check if two subtrees are mirror images of each other */
bool isMirror(struct TreeNode* root1, struct TreeNode* root2) {
    if (!root1 && !root2)
        return true;  /* Both nodes are NULL, symmetric */
    if (!root1 || !root2)
        return false; /* One is NULL and the other is not, not symmetric */
    if (root1->val != root2->val)
        return false; /* Values differ, not symmetric */

    return (isMirror(root1->left, root2->right) && /* Left of root1 vs right of root2 */
            isMirror(root1->right, root2->left));  /* Right of root1 vs left of root2 */
}

/* Check if a binary tree is symmetric around its center */
bool isSymmetric(struct TreeNode* root) {
    return isMirror(root->left, root->right); /* Compare left and right subtrees */
}
```
