[733. Flood Fill](https://leetcode.com/problems/flood-fill/description/)

```c
/* 733. Flood Fill (Depth-First Search, DFS) */
int **dfs(int** image, int m, int n, int i, int j, int color, int orign, bool **visited) {
    /* Check whether the current pixel has the original color */
    if (image[i][j] == orign) {
        /* Change the current pixel to the new color */
        image[i][j] = color;

        /* Move to the upper pixel if it is inside bounds and not visited */
        if (i - 1 >= 0 && !visited[i - 1][j]) {
            visited[i - 1][j] = true;
            image = dfs(image, m, n, i - 1, j, color, orign, visited);
        }

        /* Move to the left pixel if it is inside bounds and not visited */
        if (j - 1 >= 0 && !visited[i][j - 1]) {
            visited[i][j - 1] = true;
            image = dfs(image, m, n, i, j - 1, color, orign, visited);
        }

        /* Move to the lower pixel if it is inside bounds and not visited */
        if (i + 1 < m && !visited[i + 1][j]) {
            visited[i + 1][j] = true;
            image = dfs(image, m, n, i + 1, j, color, orign, visited);
        }

        /* Move to the right pixel if it is inside bounds and not visited */
        if (j + 1 < n && !visited[i][j + 1]) {
            visited[i][j + 1] = true;
            image = dfs(image, m, n, i, j + 1, color, orign, visited);
        }
    }

    /* Return the updated image after DFS processing */
    return image;
}

/*
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced,
 * assume caller calls free().
 *
 * Algorithm: Depth-First Search (DFS) with a visited matrix
 */
int** floodFill(int** image, int imageSize, int* imageColSize, int sr, int sc, int color, int* returnSize, int** returnColumnSizes) {
    /* Allocate a 2D visited array to mark processed pixels */
    bool **visited = (bool **)malloc(imageSize * sizeof(bool *));

    /* Initialize each row of the visited array to false */
    for (int i = 0; i < imageSize; i++)
        visited[i] = (bool *)calloc((*imageColSize), sizeof(bool));

    /* Set the number of rows for the returned image */
    *returnSize = imageSize;

    /* Allocate and initialize the column sizes for each row */
    *returnColumnSizes = (int *)malloc(imageSize * sizeof(int));
    for (int i = 0; i < imageSize; i++)
        (*returnColumnSizes)[i] = *imageColSize;

    /* Mark the starting pixel as visited */
    visited[sr][sc] = true;

    /* Perform DFS starting from the source pixel */
    image = dfs(image, imageSize, *imageColSize, sr, sc, color, image[sr][sc], visited);

    /* Free the visited array memory */
    for (int i = 0; i < imageSize; i++)
        free(visited[i]);
    free(visited);

    /* Return the flood-filled image */
    return image;
}
```

```c
/* 733. Flood Fill — Breadth-First Search (BFS) */

typedef struct Queue {
    int **arr;          /* Queue array storing coordinate pairs */
    int capacity;       /* Maximum number of elements in the queue */
    int front;          /* Index before the first valid element */
    int rear;           /* Index of the next insertion position */
} queue;

/* Initialize a queue with given capacity */
queue *init(int capacity) {
    queue *q = (queue *)malloc(sizeof(queue));

    if (q) {
        /* Allocate memory for coordinate pairs */
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
    if (q->arr) {
        for (int i = 0; i < q->capacity; i++)
            free(q->arr[i]);
        free(q->arr);
    }
    free(q);
}

/* Push a coordinate (i, j) into the queue */
bool push(queue *q, int i, int j) {
    if (q->rear >= q->capacity)
        return false;

    q->arr[q->rear][0] = i;
    q->arr[q->rear][1] = j;
    q->rear++;

    return true;
}

/* Pop a coordinate (i, j) from the queue */
bool pop(queue *q, int *i, int *j) {
    if (q->front + 1 == q->rear)
        return false;

    q->front++;
    *i = q->arr[q->front][0];
    *j = q->arr[q->front][1];

    return true;
}

/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
/*
 * Perform flood fill on the image
 * Algorithm: Breadth-First Search (BFS)
 * The BFS starts from (sr, sc) and expands to all 4-directionally connected
 * pixels that have the same original color
 */
int** floodFill(int** image, int imageSize, int* imageColSize, int sr, int sc, int color, int* returnSize, int** returnColumnSizes) {
    queue *q = init(imageSize * (*imageColSize)); /* Queue for BFS traversal */
    bool **visited = (bool **)malloc(imageSize * sizeof(bool *)); /* Visited matrix */
    int orgin = image[sr][sc]; /* Original color at the starting pixel */

    /* Initialize visited matrix */
    for (int i = 0; i < imageSize; i++)
        visited[i] = (bool *)calloc(*imageColSize, sizeof(bool));

    /* Set return size information as required by the problem */
    *returnSize = imageSize;
    *returnColumnSizes = (int *)malloc(imageSize * sizeof(int));
    for (int i = 0; i < imageSize; i++)
        (*returnColumnSizes)[i] = *imageColSize;

    /* Start BFS from the source pixel */
    push(q, sr, sc);
    visited[sr][sc] = true;
    while (q->front + 1 < q->rear) {
        int i = 0;
        int j = 0;

        pop(q, &i, &j);
        if (image[i][j] == orgin) {
            /* Change the pixel color */
            image[i][j] = color;

            /* Check and push neighboring pixels */
            if (i - 1 >= 0 && !visited[i - 1][j]) {
                push(q, i - 1, j);
                visited[i - 1][j] = true;
            }
            if (j - 1 >= 0 && !visited[i][j - 1]) {
                push(q, i, j - 1);
                visited[i][j - 1] = true;
            }
            if (i + 1 < imageSize && !visited[i + 1][j]) {
                push(q, i + 1, j);
                visited[i + 1][j] = true;
            }
            if (j + 1 < (*imageColSize) && !visited[i][j + 1]) {
                push(q, i, j + 1);
                visited[i][j + 1] = true;
            }
        }
    }

    /* Free visited matrix and queue */
    for (int i = 0; i < imageSize; i++)
        free(visited[i]);
    free(visited);
    release(q);

    return image;
}
```
