[994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/description/)

```c
/* 994. Rotting Oranges - Multi-Source Breadth-First Search (BFS) */

typedef struct Queue {
    int **arr;      /* Store coordinate pairs (i, j) */
    int capacity;   /* Maximum queue size */
    int front;      /* Index of the front element */
    int rear;       /* Index of the next insertion */
} queue;

queue *init(int capacity) {
    /* Initialize queue */
    queue *q = (queue *)malloc(sizeof(queue));

    if (q) {
        q->arr = (int **)malloc(capacity * sizeof(int *));
        for (int i = 0; i < capacity; i++)
            q->arr[i] = (int *)calloc(2, sizeof(int));
        q->capacity = capacity;
        q->front = 0;
        q->rear = 0;
    }

    return q;
}

void release(queue *q) {
    /* Free queue memory */
    if (q->arr) {
        for (int i = 0; i < q->capacity; i++)
            free(q->arr[i]);
        free(q->arr);
    }
    free(q);
}

bool enqueue(queue *q, int i, int j) {
    /* Push a coordinate pair into the queue */
    if (q->rear >= q->capacity)
        return false;

    q->arr[q->rear][0] = i;
    q->arr[q->rear][1] = j;
    q->rear++;

    return true;    
}

bool dequeue(queue *q, int *i, int *j) {
    /* Pop a coordinate pair from the queue */
    if (q->front >= q->rear)
        return false;

    *i = q->arr[q->front][0];
    *j = q->arr[q->front][1];
    q->front++;

    return true;
}

int orangesRotting(int** grid, int gridSize, int* gridColSize) {
    /* Initialize queue and visited time matrix */
    queue *q = init(gridSize * (*gridColSize));
    int **visited = (int **)malloc(gridSize * sizeof(int *));
    int minutes = 0;

    /* visited[i][j] stores the minute when the orange becomes rotten */
    for (int i = 0; i < gridSize; i++) {
        visited[i] = (int *)malloc((*gridColSize) * sizeof(int));
        for (int j = 0; j < (*gridColSize); j++)
            visited[i][j] = -1;
    }

    /* Enqueue all initially rotten oranges (multi-source BFS) */
    for (int i = 0; i < gridSize; i++) {
        for (int j = 0; j < (*gridColSize); j++) {
            if (grid[i][j] == 2) {
                visited[i][j] = 0;
                enqueue(q, i, j);
            }
        }
    }

    /* BFS traversal */
    while (q->front < q->rear) {
        int i = 0;
        int j = 0;

        dequeue(q, &i, &j);

        /* Check four directions */
        if (i - 1 >= 0 && grid[i-1][j] == 1 && visited[i-1][j] < 0) {
            visited[i-1][j] = visited[i][j] + 1;
            grid[i-1][j] = 2;
            enqueue(q, i - 1, j);
        }
        if (j - 1 >= 0 && grid[i][j-1] == 1 && visited[i][j-1] < 0) {
            visited[i][j-1] = visited[i][j] + 1;
            grid[i][j-1] = 2;
            enqueue(q, i, j - 1);
        }
        if (i + 1 < gridSize && grid[i+1][j] == 1 && visited[i+1][j] < 0) {
            visited[i+1][j] = visited[i][j] + 1;
            grid[i+1][j] = 2;
            enqueue(q, i + 1, j);
        }
        if (j + 1 < (*gridColSize) && grid[i][j+1] == 1 && visited[i][j+1] < 0) {
            visited[i][j+1] = visited[i][j] + 1;
            grid[i][j+1] = 2;
            enqueue(q, i, j + 1);
        }
    }

    /* Compute the maximum minutes needed and check if fresh oranges remain */
    for (int i = 0; i < gridSize; i++) {
        for (int j = 0; j < (*gridColSize); j++) {
            if (grid[i][j] == 1) {
                minutes = -1;
                goto free_alloc;
            }
            if (minutes < visited[i][j])
                minutes = visited[i][j];
        }
    }

free_alloc:
    /* Free allocated memory */
    for (int i = 0; i < gridSize; i++)
        free(visited[i]);
    free(visited);
    release(q);

    return minutes;
}
```
