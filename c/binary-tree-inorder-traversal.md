[94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)

```c
/* 94. Binary Tree Inorder Traversal */

/* Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Define a stack structure to assist with iterative inorder traversal */
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

/* Perform inorder traversal iteratively using a stack
 * Return an array containing the traversal result
 */
int* inorderTraversal(struct TreeNode* root, int* returnSize) {
    *returnSize = 0;
    if (!root)
        return NULL;

    int *arr = (int *)malloc(100 * sizeof(int)); /* Array to store result */
    stack *s = init(100); /* Initialize stack */

    /* Traverse the tree */
    while (root || s->top != 0) {
        if (root) {
            push(s, root);      /* Go as left as possible */
            root = root->left;
            continue;
        }

        pop(s, &root);          /* Visit node */
        arr[*returnSize] = root->val;
        (*returnSize)++;

        root = root->right;     /* Move to right subtree */
    }

    release(s); /* Free stack memory */

    return arr;
}
```

```c
/* 94. Binary Tree Inorder Traversal */

/* Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Recursive helper function to perform inorder traversal
 * Visit left subtree → current node → right subtree
 */
void inorder(struct TreeNode *root, int *returnSize, int *arr) {
    if (!root)
        return; /* Base case: empty subtree */

    inorder(root->left, returnSize, arr); /* Traverse left subtree */

    arr[*returnSize] = root->val; /* Visit current node */
    (*returnSize)++;

    inorder(root->right, returnSize, arr); /* Traverse right subtree */
}

/* Main function to perform inorder traversal
 * Returns an array containing the traversal result
 */
int* inorderTraversal(struct TreeNode* root, int* returnSize) {
    *returnSize = 0;
    if (!root)
        return NULL; /* Handle empty tree */

    int *arr = (int *)malloc(100 * sizeof(int)); /* Allocate space for result */

    inorder(root, returnSize, arr); /* Perform recursive traversal */

    return arr; /* Return the traversal result */
}
```
