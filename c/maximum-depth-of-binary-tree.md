[104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)

```c
/* 104. Maximum Depth of Binary Tree */

/* Definition for a binary tree node */
/* struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Define a circular queue structure to assist BFS traversal */
typedef struct Queue {
    struct TreeNode **nodes; /* Array to store TreeNode pointers */
    int capacity;            /* Maximum capacity of the queue */
    int front;               /* Index of the front element */
    int rear;                /* Index of the next insertion position */
} queue;

/* Initialize a queue with given capacity */
queue *init(int capacity) {
    queue *q = (queue *)malloc(sizeof(queue));

    if (q) {
        q->nodes = (struct TreeNode **)malloc((capacity + 1) * sizeof(struct TreeNode *)); /* Allocate memory for node pointers */
        q->capacity = capacity + 1;  /* One extra slot to distinguish full vs empty */
        q->front = 0;                /* Initialize front index */
        q->rear = 0;                 /* Initialize rear index */
    }

    return q;
}

/* Release the memory allocated for the queue */
void release(queue *q) {
    if (q) {
        if (q->nodes)
            free(q->nodes); /* Free the node array */
        free(q);            /* Free the queue structure */
    }
}

/* Push a TreeNode into the queue */
bool push(queue *q, struct TreeNode *node) {
    if ((q->rear + 1) % q->capacity == q->front)
        return false; /* Queue is full */

    q->nodes[q->rear] = node;           /* Insert node at rear */
    q->rear = (q->rear + 1) % q->capacity; /* Move rear index */

    return true;
}

/* Pop a TreeNode from the queue */
bool pop(queue *q, struct TreeNode **node) {
    if (q->front == q->rear)
        return false; /* Queue is empty */

    *node = q->nodes[q->front];        /* Retrieve node at front */
    q->front = (q->front + 1) % q->capacity; /* Move front index */

    return true;
}

/* Calculate the maximum depth of a binary tree using level-order traversal (BFS) */
int maxDepth(struct TreeNode* root) {
    int height = 0;
    queue *q = init(40000); /* Initialize queue with sufficient capacity */

    if (!root)
        return 0;           /* Empty tree has depth 0 */

    push(q, root);          /* Enqueue root node */

    while (q->front != q->rear) {  /* Continue until queue is empty */
        int levelSize = q->rear - q->front; /* Number of nodes at current level */

        for (int i = 0; i != levelSize; i++) {
            struct TreeNode *node = NULL;
            pop(q, &node);              /* Dequeue one node */

            if (node->left)
                push(q, node->left);    /* Enqueue left child */
            if (node->right)
                push(q, node->right);   /* Enqueue right child */
        }

        height++; /* Increment height after processing one level */
    }

    release(q); /* Free queue memory */

    return height; /* Return maximum depth */
}
```

```c
/* 104. Maximum Depth of Binary Tree */

/* Definition for a binary tree node */
/* struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

/* Recursively calculate the maximum depth of a binary tree */
int maxDepth(struct TreeNode* root) {
    int height = 0;

    if (!root)
        return 0; /* Base case: empty tree has depth 0 */

    int left = maxDepth(root->left);   /* Recursively find depth of left subtree */
    int right = maxDepth(root->right); /* Recursively find depth of right subtree */

    /* Return the larger depth between left and right, plus 1 for current node */
    return (left > right) ? (left + 1) : (right + 1);
}
```
