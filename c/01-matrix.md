[542. 01 Matrix](https://leetcode.com/problems/01-matrix/description/)

```c
/* 542. 01 Matrix - Multi-Source Breadth-First Search (BFS) */

typedef struct Queue {
    int **arr;      /* 2D array used to store coordinate pairs (i, j) */
    int capacity;   /* Maximum number of elements the queue can hold */
    int front;      /* Index of the front element */
    int rear;       /* Index of the next insertion position */
} queue;

queue *init(int capacity) {
    /* Initialize a queue with given capacity */
    queue *q = (queue *)malloc(sizeof(queue));

    if (q) {
        q->arr = (int **)malloc(capacity * sizeof(int *));
        for (int i = 0; i < capacity; i++)
            q->arr[i] = malloc(2 * sizeof(int));
        q->capacity = capacity;
        q->front = 0;
        q->rear = 0;
    }

    return q;
}

void release(queue *q) {
    /* Free all dynamically allocated memory of the queue */
    if (q->arr) {
        for (int i = 0; i < q->capacity; i++)
            free(q->arr[i]);
        free(q->arr);
    }
    free(q);
}

bool enqueue(queue *q, int i, int j) {
    /* Insert a coordinate pair (i, j) into the queue */
    if (q->rear == q->capacity)
        return false;

    q->arr[q->rear][0] = i;
    q->arr[q->rear][1] = j;
    q->rear++;

    return true;
}

bool dequeue(queue *q, int *i, int *j) {
    /* Remove a coordinate pair (i, j) from the queue */
    if (q->front >= q->rear)
        return false;

    *i = q->arr[q->front][0];
    *j = q->arr[q->front][1];
    q->front++;

    return true;
}

/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
int** updateMatrix(int** mat, int matSize, int* matColSize, int* returnSize, int** returnColumnSizes) {
    /* Initialize queue for BFS traversal */
    queue *q = init(matSize * (*matColSize));

    /* Distance matrix to store the minimum distance to nearest 0 */
    int **distance = (int **)malloc(matSize * sizeof(int *));
    /* Visited matrix to avoid revisiting cells */
    bool **visited = (bool **)malloc(matSize * sizeof(bool *));

    /* Initialize return sizes */
    *returnSize = matSize;
    *returnColumnSizes = (int *)calloc(matSize, sizeof(int));
    for (int i = 0; i < matSize; i++) {
        distance[i] = (int *)calloc((*matColSize), sizeof(int));
        visited[i] = (bool *)calloc((*matColSize), sizeof(bool));
        (*returnColumnSizes)[i] = *matColSize;
    }

    /* Multi-source BFS initialization: enqueue all cells with value 0 */
    for (int i = 0; i < matSize; i++) {
        for (int j = 0; j < *matColSize; j++) {
            if (mat[i][j] == 0) {
                visited[i][j] = true;
                enqueue(q, i, j);
            }
        }
    }

    /* Perform BFS to compute shortest distance to the nearest 0 for each cell */
    while (q->front < q->rear) {
        int i = 0;
        int j = 0;

        dequeue(q, &i, &j);

        /* Explore the four adjacent directions */
        if (i - 1 >= 0 && mat[i - 1][j] != 0 && !visited[i - 1][j]) {
            visited[i - 1][j] = true;
            distance[i - 1][j] = distance[i][j] + 1;
            enqueue(q, i - 1, j);
        }
        if (j - 1 >= 0 && mat[i][j - 1] != 0 && !visited[i][j - 1]) {
            visited[i][j - 1] = true;
            distance[i][j - 1] = distance[i][j] + 1;
            enqueue(q, i, j - 1);
        }
        if (i + 1 < matSize && mat[i + 1][j] != 0 && !visited[i + 1][j]) {
            visited[i + 1][j] = true;
            distance[i + 1][j] = distance[i][j] + 1;
            enqueue(q, i + 1, j);
        }
        if (j + 1 < *matColSize && mat[i][j + 1] != 0 && !visited[i][j + 1]) {
            visited[i][j + 1] = true;
            distance[i][j + 1] = distance[i][j] + 1;
            enqueue(q, i, j + 1);
        }
    }

    /* Release auxiliary memory */
    release(q);
    for (int i = 0; i < matSize; i++)
        free(visited[i]);
    free(visited);

    return distance;
}
```
