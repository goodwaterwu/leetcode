[102. Binary Tree Level Order Traversal](binary-tree-level-order-traversal)

```c
/* 102. Binary Tree Level Order Traversal */

/* Definition for a binary tree node */
/* struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Define a circular queue structure for BFS traversal */
typedef struct Queue {
    struct TreeNode **nodes; /* Array of pointers to TreeNode */
    int capacity;            /* Maximum capacity of the queue */
    int front;               /* Index of the front element */
    int rear;                /* Index of the next insertion position */
} queue;

/* Initialize a queue with given capacity */
queue *init(int capacity) {
    queue *q = (queue *)malloc(sizeof(queue));

    if (q) {
        q->nodes = (struct TreeNode **)malloc((capacity + 1) * sizeof(struct TreeNode *)); /* Allocate array for nodes */
        q->capacity = capacity + 1; /* One extra slot to distinguish full vs empty */
        q->front = 0;               /* Initialize front index */
        q->rear = 0;                /* Initialize rear index */
    }

    return q;
}

/* Release memory allocated for the queue */
void release(queue *q) {
    if (q) {
        if (q->nodes)
            free(q->nodes); /* Free node array */
        free(q);            /* Free queue structure */
    } 
}

/* Push a node into the queue */
bool push(queue *q, struct TreeNode *node) {
    if ((q->rear + 1) % q->capacity == q->front)
        return false; /* Queue is full */

    q->nodes[q->rear] = node; /* Insert node */
    q->rear++;                /* Advance rear pointer (non-wrapping in this case) */

    return true;
}

/* Pop a node from the queue */
bool pop(queue *q, struct TreeNode **node) {
    if (q->front == q->rear)
        return false; /* Queue is empty */

    *node = q->nodes[q->front]; /* Retrieve node */
    q->front++;                 /* Advance front pointer */

    return true;
}

/* Perform level-order traversal (BFS) and return a 2D array of values by levels */
/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
int** levelOrder(struct TreeNode* root, int* returnSize, int** returnColumnSizes) {
    *returnSize = 0;             /* Initialize return size */
    if (!root)
        return NULL;             /* Empty tree returns NULL */

    int **arr = (int **)malloc(2000 * sizeof(int *)); /* Allocate memory for result array */
    *returnColumnSizes = (int *)malloc(2000 * sizeof(int)); /* Allocate memory for column sizes */
    queue *q = init(2000);       /* Initialize queue */
    push(q, root);               /* Enqueue root node */

    while (q->front != q->rear) { /* Continue until queue is empty */
        int levelSize = q->rear - q->front; /* Number of nodes at current level */

        arr[*returnSize] = (int *)malloc(levelSize * sizeof(int)); /* Allocate array for current level */
        (*returnColumnSizes)[*returnSize] = levelSize;              /* Record column size for current level */

        for (int i = 0; i != levelSize; i++) {
            struct TreeNode *node = NULL;
            pop(q, &node); /* Dequeue node */

            arr[*returnSize][i] = node->val; /* Store node value */

            if (node->left)
                push(q, node->left);  /* Enqueue left child */
            if (node->right)
                push(q, node->right); /* Enqueue right child */
        }

        (*returnSize)++; /* Move to next level */
    }

    release(q); /* Free queue memory */

    return arr; /* Return 2D level order result */
}
```
