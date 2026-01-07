[133. Clone Graph](https://leetcode.com/problems/clone-graph/description/)

```c
/* 133. Clone Graph */

/**
 * Definition for a Node.
 * struct Node {
 *     int val;
 *     int numNeighbors;
 *     struct Node** neighbors;
 * };
 */

/*
 * Stack structure for iterative DFS.
 * nodes    : array of pointers to nodes in the graph
 * capacity : maximum number of nodes that can be stored
 * top      : index of next free position (also represents stack size)
 */
typedef struct Stack {
    struct Node **nodes;
    int capacity;
    int top;
} stack;

/* Initialize a stack with the given capacity */
stack *init(int capacity) {
    stack *s = (stack *)malloc(sizeof(stack));
    if (s) {
        s->nodes = (struct Node **)malloc(capacity * sizeof(struct Node *));
        s->capacity = capacity;
        s->top = 0;
    }
    return s;
}

/* Release memory associated with the stack */
void release(stack *s) {
    if (s->nodes)
        free(s->nodes);
    free(s);
}

/* Push a node onto the stack */
bool push(stack *s, struct Node *node) {
    if (s->top == s->capacity)
        return false;
    s->nodes[s->top++] = node;
    return true;
}

/* Pop the top node from the stack */
bool pop(stack *s, struct Node **node) {
    if (s->top == 0)
        return false;
    s->top--;
    *node = s->nodes[s->top];
    return true;
}

/*
 * Clone an undirected graph given its starting node.
 * Returns a deep copy of the graph.
 */
struct Node *cloneGraph(struct Node *s) {
    if (!s)
        return NULL;

    /* Array to keep track of cloned nodes (indexed by node value) */
    struct Node *visited[101];
    memset(visited, 0, sizeof(visited));

    /* Stack for iterative DFS */
    stack *stk = init(100);

    /* Start DFS from the source node */
    push(stk, s);

    while (stk->top > 0) {
        struct Node *n = NULL;
        struct Node *copy = NULL;

        /* Get next node to process */
        pop(stk, &n);

        /* If the node hasn't been cloned yet, allocate memory */
        copy = visited[n->val];
        if (!copy)
            copy = (struct Node *)calloc(1, sizeof(struct Node));

        /* Copy node's value and neighbor count */
        copy->val = n->val;
        copy->numNeighbors = n->numNeighbors;

        /* Allocate array for neighbors in the cloned node */
        copy->neighbors = (struct Node **)malloc(n->numNeighbors * sizeof(struct Node *));
        visited[n->val] = copy;

        /* Iterate through neighbors to clone them */
        for (int i = 0; i < n->numNeighbors; i++) {
            if (visited[n->neighbors[i]->val]) {
                /* Neighbor already cloned, link it */
                copy->neighbors[i] = visited[n->neighbors[i]->val];
            } else {
                /* Neighbor not cloned yet, allocate and push to stack */
                struct Node *neighbor = (struct Node *)calloc(1, sizeof(struct Node));
                visited[n->neighbors[i]->val] = neighbor;
                push(stk, n->neighbors[i]);
                copy->neighbors[i] = neighbor;
            }
        }
    }

    /* Free the DFS stack */
    release(stk);

    /* Return the cloned node corresponding to the original starting node */
    return visited[s->val];
}
```

```c
/* 133. Clone Graph */

/**
 * Definition for a Node.
 * struct Node {
 *     int val;
 *     int numNeighbors;
 *     struct Node** neighbors;
 * };
 */

/*
 * Recursive DFS function to clone a node and its neighbors.
 * s       : the original node to clone
 * visited : array storing cloned nodes indexed by their value
 *
 * Returns a pointer to the cloned node corresponding to s.
 */
struct Node *dfs(struct Node *s, struct Node *visited[101]) {
    /* If this node has not been cloned yet */
    if (!visited[s->val]) {
        /* Allocate memory for the clone */
        struct Node *node = (struct Node *)calloc(1, sizeof(struct Node));
        node->val = s->val;
        node->numNeighbors = s->numNeighbors;
        node->neighbors = (struct Node **)calloc(node->numNeighbors, sizeof(struct Node *));
        visited[s->val] = node;

        /* Recursively clone all neighbors */
        for (int i = 0; i < node->numNeighbors; i++) {
            dfs(s->neighbors[i], visited);
            node->neighbors[i] = visited[s->neighbors[i]->val];
        }
    }

    /* Return the cloned node */
    return visited[s->val];
}

/*
 * Clone an undirected graph starting from node s.
 * Uses a recursive DFS approach with a visited array to avoid cycles.
 */
struct Node *cloneGraph(struct Node *s) {
    if (!s)
        return NULL;

    /* Array to keep track of cloned nodes (indexed by node value) */
    struct Node *visited[101];
    memset(visited, 0, sizeof(visited));

    /* Start DFS cloning from the source node */
    return dfs(s, visited);
}
```
