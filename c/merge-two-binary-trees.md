[617. Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees/description/)

```c
/* 617. Merge Two Binary Trees */
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Recursively merge two binary trees node by node */
struct TreeNode* mergeTrees(struct TreeNode* root1, struct TreeNode* root2) {
    /* If both trees are empty, return NULL */
    if (!root1 && !root2)
        return NULL;

    /* If the first tree is empty, create a new node from the second tree */
    if (!root1) {
        root1 = (struct TreeNode *)malloc(sizeof(struct TreeNode));
        root1->val = root2->val;
        root1->left = mergeTrees(NULL, root2->left);
        root1->right = mergeTrees(NULL, root2->right);
        return root1;
    }

    /* If the second tree is empty, return the first tree as is */
    if (!root2)
        return root1;

    /* Merge the values of overlapping nodes */
    root1->val += root2->val;

    /* Recursively merge the left and right subtrees */
    root1->left = mergeTrees(root1->left, root2->left);
    root1->right = mergeTrees(root1->right, root2->right);

    /* Return the merged tree */
    return root1;
}
```
