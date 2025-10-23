[590. N-ary Tree Postorder Traversal](https://leetcode.com/problems/n-ary-tree-postorder-traversal/description/)

```c
/* 590. N-ary Tree Postorder Traversal */

/* Definition for a Node.
 * struct Node {
 *     int val;
 *     int numChildren;
 *     struct Node** children;
 * };
 */

/* Define a stack structure to assist with iterative traversal */
typedef struct Stack {
    struct Node **nodes;
    int capacity;
    int top;
} stack;

/* Initialize a stack with given capacity */
stack *init(int capacity) {
    stack *s = (stack *)malloc(sizeof(stack));

    if (s) {
        s->nodes = (struct Node **)malloc(capacity * sizeof(struct Node *));
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

/* Push a Node pointer onto the stack */
bool push(stack *s, struct Node *node) {
    if (s->top == s->capacity)
        return false;

    s->nodes[s->top] = node;
    s->top++;

    return true;
}

/* Pop a Node pointer from the stack */
bool pop(stack *s, struct Node **node) {
    if (s->top == 0)
        return false;

    s->top--;
    *node = s->nodes[s->top];

    return true;
}

/* Perform postorder traversal of an N-ary tree iteratively using a stack
 * Note: Traversal is done in root→children order first, then reversed to get postorder
 */
int* postorder(struct Node* root, int* returnSize) {
    *returnSize = 0;
    if (!root)
        return NULL; /* Empty tree */

    int *arr = (int *)malloc(100000 * sizeof(int)); /* Array to store traversal */
    stack *s = init(100000); /* Initialize stack */

    push(s, root);
    while (s->top != 0) {
        pop(s, &root);
        arr[*returnSize] = root->val; /* Visit root first */
        (*returnSize)++;

        /* Push children to stack */
        for (int i = 0; i != root->numChildren; i++)
            push(s, root->children[i]);
    }

    release(s); /* Free stack memory */

    /* Reverse array to get postorder (children → root) */
    int i = 0;
    int j = (*returnSize) - 1;
    while (i < j) {
        arr[i] = arr[i] ^ arr[j];
        arr[j] = arr[i] ^ arr[j];
        arr[i] = arr[i] ^ arr[j];
        i++;
        j--;
    }

    return arr; /* Return postorder traversal */
}
```

```c
/* 590. N-ary Tree Postorder Traversal */

/**
 * Definition for a Node.
 * struct Node {
 *     int val;
 *     int numChildren;
 *     struct Node** children;
 * };
 */

void post(struct Node* root, int* returnSize, int *arr) {
    if (!root)
        return; /* Base case: if the current node is NULL, stop recursion */

    /* Recursively traverse all children first */
    for (int i = 0; i != root->numChildren; i++)
        post(root->children[i], returnSize, arr);

    /* After visiting all children, record the current node's value */
    arr[*returnSize] = root->val;
    (*returnSize)++;
}

/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* postorder(struct Node* root, int* returnSize) {
    *returnSize = 0; /* Initialize traversal size to zero */
    if (!root)
        return NULL; /* Empty tree, return NULL */

    int *arr = (int *)malloc(100000 * sizeof(int)); /* Allocate memory for traversal result */

    post(root, returnSize, arr); /* Perform recursive postorder traversal */

    return arr; /* Return the array containing the traversal result */
}
```
