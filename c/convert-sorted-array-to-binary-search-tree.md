[108. Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/description/)

```c
/* 108. Convert Sorted Array to Binary Search Tree */

/* Definition for a binary tree node */
/* struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Recursively convert a sorted array into a height-balanced BST */
struct TreeNode* sortedArrayToBST(int* nums, int numsSize) {
    if (numsSize == 0)
        return NULL; /* Base case: empty array returns NULL */

    struct TreeNode *root = (struct TreeNode *)malloc(sizeof(struct TreeNode)); /* Allocate memory for new node */
    int i = 0;
    int j = numsSize - 1;
    int m = i + (j - i) / 2; /* Find the middle index */

    root->val = nums[m]; /* Set the middle element as root node value */

    /* Recursively build left and right subtrees */
    root->left = sortedArrayToBST(nums, m);             /* Left subtree: elements before middle */
    root->right = sortedArrayToBST(nums + m + 1, j - m);/* Right subtree: elements after middle */

    return root; /* Return the root node */
}
```
