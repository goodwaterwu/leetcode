[230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/)

```c
/* 230. Kth Smallest Element in a BST */
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

void findkthSmallest(struct TreeNode *root, int k, struct TreeNode *node, int *count) {
    /* If the current node is NULL, stop traversal */
    if (!root)
        return;

    /* Continue traversal only if the kth element has not been found yet */
    if (*count < k) {
        /* In-order traversal: visit left subtree first */
        findkthSmallest(root->left, k, node, count);

        /* Increment count when visiting the current node */
        (*count)++;

        /* If the current node is the kth smallest element */
        if (*count == k) {
            /* Store the value and pointers of the kth node */
            node->val = root->val;
            node->left = root->left;
            node->right = root->right;
            return;
        }

        /* Continue traversal in the right subtree */
        findkthSmallest(root->right, k, node, count);
    }
}

int kthSmallest(struct TreeNode* root, int k) {
    /* Temporary node used to store the kth smallest element */
    struct TreeNode node;

    /* Counter to track the number of visited nodes */
    int count = 0;

    /* Perform in-order traversal to find the kth smallest element */
    findkthSmallest(root, k, &node, &count);

    /* Return the value of the kth smallest element */
    return node.val;
}
```
