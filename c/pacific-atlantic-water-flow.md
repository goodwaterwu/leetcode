[417. Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/description/)

```c
/* 417. Pacific Atlantic Water Flow — BFS from Ocean Borders */

typedef struct Queue {
    int **arr;
    int capacity;
    int front;
    int rear;
} queue;

/* Initialize a queue that stores coordinate pairs (x, y) */
queue *init(int capacity) {
    queue *q = (queue *)malloc(sizeof(queue));

    if (q) {
        /* Allocate space for coordinates */
        q->arr = (int **)malloc(capacity * sizeof(int *));
        for (int i = 0; i < capacity; i++)
            q->arr[i] = (int *)calloc(2, sizeof(int));
        q->capacity = capacity;
        q->front = -1;
        q->rear = 0;
    }

    return q;
}

/* Release all memory allocated for the queue */
void release(queue *q) {
    if (q) {
        for (int i = 0; i < q->capacity; i++)
            free(q->arr[i]);
        free(q->arr);
    }
    free(q);
}

/* Push a coordinate (x, y) into the queue */
bool push(queue *q, int x, int y) {
    if (q->rear == q->capacity)
        return false;

    q->arr[q->rear][0] = x;
    q->arr[q->rear][1] = y;
    q->rear++;

    return true;
}

/* Pop a coordinate (x, y) from the queue */
bool pop(queue *q, int *x, int *y) {
    if (q->front == q->rear - 1)
        return false;

    q->front++;
    *x = q->arr[q->front][0];
    *y = q->arr[q->front][1];

    return true;
}

/*
 * Perform BFS to find all reachable coordinates
 * Algorithm: Breadth-First Search (Reverse Flow)
 * Rule: Water can flow from lower or equal height to higher or equal height
 */
void get_coordinates(queue *q, int **h, int m, int n, bool **flow) {
    while (q->front < q->rear - 1) {
        int x = 0;
        int y = 0;
        int i = 0;
        int j = 0;

        pop(q, &x, &y);

        /* Move right */
        i = x + 0;
        j = y + 1;
        if (0 <= i && i < m && 0 <= j && j < n && !flow[i][j] && h[i][j] >= h[x][y]) {
            push(q, i, j);
            flow[i][j] = true;
        }

        /* Move down */
        i = x + 1;
        j = y + 0;
        if (0 <= i && i < m && 0 <= j && j < n && !flow[i][j] && h[i][j] >= h[x][y]) {
            push(q, i, j);
            flow[i][j] = true;
        }

        /* Move left */
        i = x + 0;
        j = y - 1;
        if (0 <= i && i < m && 0 <= j && j < n && !flow[i][j] && h[i][j] >= h[x][y]) {
            push(q, i, j);
            flow[i][j] = true;
        }

        /* Move up */
        i = x - 1;
        j = y + 0;
        if (0 <= i && i < m && 0 <= j && j < n && !flow[i][j] && h[i][j] >= h[x][y]) {
            push(q, i, j);
            flow[i][j] = true;
        }
    }
}

/*
 * Return coordinates where water can flow to both the Pacific and Atlantic oceans
 * Algorithm:
 * - BFS from Pacific borders
 * - BFS from Atlantic borders
 * - Intersection of reachable cells
 */
int** pacificAtlantic(int** heights, int heightsSize, int* heightsColSize, int* returnSize, int** returnColumnSizes) {
    queue *q_pacific = init(heightsSize * (*heightsColSize));
    queue *q_atlantic = init(heightsSize * (*heightsColSize));
    int **arr = (int **)malloc(heightsSize * (*heightsColSize) * sizeof(int *));
    bool **flow_pacific = (bool **)malloc(heightsSize * sizeof(bool *));
    bool **flow_atlantic = (bool **)malloc(heightsSize * sizeof(bool *));

    /* Allocate result array */
    for (int i = 0; i < heightsSize * (*heightsColSize); i++)
        arr[i] = (int *)calloc(2, sizeof(int));

    /* Initialize visited matrices */
    for (int i = 0; i < heightsSize; i++) {
        flow_pacific[i] = (bool *)calloc((*heightsColSize), sizeof(bool));
        flow_atlantic[i] = (bool *)calloc((*heightsColSize), sizeof(bool));
    }

    (*returnSize) = 0;

    /* Add Pacific border cells */
    for (int i = 0; i < heightsSize; i++) {
        push(q_pacific, i, 0);
        flow_pacific[i][0] = true;
        push(q_atlantic, i, (*heightsColSize) - 1);
        flow_atlantic[i][(*heightsColSize) - 1] = true;
    }

    /* Add Atlantic border cells */
    for (int i = 0; i < *heightsColSize; i++) {
        push(q_pacific, 0, i);
        flow_pacific[0][i] = true;
        push(q_atlantic, heightsSize - 1, i);
        flow_atlantic[heightsSize - 1][i] = true;
    }

    /* BFS traversal for both oceans */
    get_coordinates(q_pacific, heights, heightsSize, *heightsColSize, flow_pacific);
    get_coordinates(q_atlantic, heights, heightsSize, *heightsColSize, flow_atlantic);

    /* Collect cells reachable by both oceans */
    for (int i = 0; i < heightsSize; i++) {
        for (int j = 0; j < (*heightsColSize); j++) {
            if (flow_pacific[i][j] && flow_atlantic[i][j]) {
                arr[*returnSize][0] = i;
                arr[*returnSize][1] = j;
                (*returnSize)++;
            }
        }
    }

    /* Set column sizes */
    *returnColumnSizes = (int *)malloc((*returnSize) * sizeof(int));
    for (int i = 0; i < *returnSize; i++)
        (*returnColumnSizes)[i] = 2;

    /* Free allocated memory */
    release(q_pacific);
    release(q_atlantic);
    for (int i = 0; i < heightsSize; i++) {
        free(flow_pacific[i]);
        free(flow_atlantic[i]);
    }
    free(flow_pacific);
    free(flow_atlantic);

    return arr;
}
```

```c
/* 417. Pacific Atlantic Water Flow — DFS (Reverse Flow) */

/*
 * Depth-First Search to mark reachable cells
 * Algorithm: DFS with reverse water flow
 * Rule: Can move to a neighbor cell only if its height is greater than or equal to current cell
 */
void dfs(int x, int y, int **h, int m, int n, bool **flow) {
    int i = x + 0;
    int j = y + 1;

    /* Boundary check and visited check */
    if (x < 0 || x >= m || y < 0 || y >= n || flow[x][y])
        return;

    /* Mark current cell as reachable */
    flow[x][y] = true;

    /* Move right */
    if (0 <= i && i < m && 0 <= j && j < n && !flow[i][j] && h[i][j] >= h[x][y])
        dfs(i, j, h, m, n, flow);

    /* Move down */
    i = x + 1;
    j = y + 0;
    if (0 <= i && i < m && 0 <= j && j < n && !flow[i][j] && h[i][j] >= h[x][y])
        dfs(i, j, h, m, n, flow);

    /* Move left */
    i = x + 0;
    j = y - 1;
    if (0 <= i && i < m && 0 <= j && j < n && !flow[i][j] && h[i][j] >= h[x][y])
        dfs(i, j, h, m, n, flow);

    /* Move up */
    i = x - 1;
    j = y + 0;
    if (0 <= i && i < m && 0 <= j && j < n && !flow[i][j] && h[i][j] >= h[x][y])
        dfs(i, j, h, m, n, flow);
}

/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
/*
 * Find all coordinates where water can flow to both oceans
 * Algorithm:
 * - DFS from all Pacific border cells
 * - DFS from all Atlantic border cells
 * - Take intersection of reachable cells
 */
int** pacificAtlantic(int** heights, int heightsSize, int* heightsColSize, int* returnSize, int** returnColumnSizes) {
    int **arr = (int **)malloc(heightsSize * (*heightsColSize) * sizeof(int *));
    bool **flow_pacific = (bool **)malloc(heightsSize * sizeof(bool *));
    bool **flow_atlantic = (bool **)malloc(heightsSize * sizeof(bool *));

    /* Allocate result array */
    for (int i = 0; i < heightsSize * (*heightsColSize); i++)
        arr[i] = (int *)calloc(2, sizeof(int));

    /* Initialize visited matrices */
    for (int i = 0; i < heightsSize; i++) {
        flow_pacific[i] = (bool *)calloc((*heightsColSize), sizeof(bool));
        flow_atlantic[i] = (bool *)calloc((*heightsColSize), sizeof(bool));
    }

    (*returnSize) = 0;

    /* DFS from Pacific borders (left and top edges) */
    for (int i = 0; i < heightsSize; i++)
        dfs(i, 0, heights, heightsSize, *heightsColSize, flow_pacific);
    for (int j = 1; j < *heightsColSize; j++)
        dfs(0, j, heights, heightsSize, *heightsColSize, flow_pacific);

    /* DFS from Atlantic borders (right and bottom edges) */
    for (int i = 0; i < heightsSize; i++)
        dfs(i, (*heightsColSize) - 1, heights, heightsSize, *heightsColSize, flow_atlantic);
    for (int j = 0; j < (*heightsColSize) - 1; j++)
        dfs(heightsSize - 1, j, heights, heightsSize, *heightsColSize, flow_atlantic);

    /* Collect cells reachable by both oceans */
    for (int i = 0; i < heightsSize; i++) {
        for (int j = 0; j < (*heightsColSize); j++) {
            if (flow_pacific[i][j] && flow_atlantic[i][j]) {
                arr[*returnSize][0] = i;
                arr[*returnSize][1] = j;
                (*returnSize)++;
            }
        }
    }

    /* Set column sizes */
    *returnColumnSizes = (int *)malloc((*returnSize) * sizeof(int));
    for (int i = 0; i < *returnSize; i++)
        (*returnColumnSizes)[i] = 2;

    /* Free allocated memory */
    for (int i = 0; i < heightsSize; i++) {
        free(flow_pacific[i]);
        free(flow_atlantic[i]);
    }
    free(flow_pacific);
    free(flow_atlantic);

    return arr;
}
```
