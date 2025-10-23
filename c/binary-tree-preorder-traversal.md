[144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/description/)

```c
/* 144. Binary Tree Preorder Traversal */

/* Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Define a stack structure to assist with iterative preorder traversal */
typedef struct Stack {
    struct TreeNode **nodes;
    int capacity;
    int top;
} stack;

/* Initialize a stack with given capacity */
stack *init(int capacity) {
    stack *s = (stack *)malloc(sizeof(stack));

    if (s) {
        s->nodes = (struct TreeNode **)malloc(capacity * sizeof(struct TreeNode *));
        s->capacity = capacity;
        s->top = 0;
    }

    return s;
}

/* Release memory allocated for the stack */
void release(stack *s) {
    if (s) {
        if (s->nodes)
            free(s->nodes);
        free(s);
    }
}

/* Push a TreeNode pointer onto the stack */
bool push(stack *s, struct TreeNode *node) {
    if (s->top == s->capacity)
        return false;

    s->nodes[s->top] = node;
    s->top++;

    return true;
}

/* Pop a TreeNode pointer from the stack */
bool pop(stack *s, struct TreeNode **node) {
    if (s->top == 0)
        return false;

    s->top--;
    *node = s->nodes[s->top];

    return true;
}

/* Perform preorder traversal iteratively using a stack
 * Visit order: Node → Left → Right
 * Return an array containing the traversal result
 */
int* preorderTraversal(struct TreeNode* root, int* returnSize) {
    *returnSize = 0;
    if (!root)
        return NULL; /* Empty tree case */

    int *arr = (int *)malloc(100 * sizeof(int)); /* Array to store traversal result */
    stack *s = init(100); /* Initialize stack */

    push(s, root); /* Start with root node */

    while (s->top != 0) {
        pop(s, &root); /* Visit top node */
        arr[*returnSize] = root->val;
        (*returnSize)++;

        /* Push right child first so that left child is processed first */
        if (root->right)
            push(s, root->right);

        if (root->left)
            push(s, root->left);
    }

    release(s); /* Free stack memory */

    return arr; /* Return traversal result */
}
```
```c
/* 144. Binary Tree Preorder Traversal */

/* Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Recursive helper function for preorder traversal
 * Visit order: Node → Left → Right
 */
void preorder(struct TreeNode *root, int *returnSize, int *arr) {
    if (!root)
        return; /* Base case: empty node */

    arr[*returnSize] = root->val; /* Visit current node */
    (*returnSize)++;

    preorder(root->left, returnSize, arr);  /* Traverse left subtree */
    preorder(root->right, returnSize, arr); /* Traverse right subtree */
}

/* Main function to perform preorder traversal
 * Returns an array containing the traversal result
 */
int* preorderTraversal(struct TreeNode* root, int* returnSize) {
    *returnSize = 0;
    if (!root)
        return NULL; /* Handle empty tree */

    int *arr = (int *)malloc(100 * sizeof(int)); /* Allocate space for result */

    preorder(root, returnSize, arr); /* Perform recursive preorder traversal */

    return arr; /* Return traversal result */
}
```
