[100. Same Tree](https://leetcode.com/problems/same-tree/description/)

```c
/* 100. Same Tree */
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
bool isSameTree(struct TreeNode* p, struct TreeNode* q) {
    /* If both nodes are NULL, the trees are identical at this position */
    if (!p && !q)
        return true;

    /* If only one node is NULL or values differ, trees are not the same */
    if ((p && !q) || (!p && q) || (p->val != q->val))
        return false;

    /* Recursively compare left and right subtrees */
    return (isSameTree(p->left, q->left) && isSameTree(p->right, q->right));
}
```
