[207. Course Schedule](https://leetcode.com/problems/course-schedule/description/)

```c
/* 207. Course Schedule — Topological Sort (Kahn's Algorithm using BFS) */

typedef struct Queue {
    int *arr;
    int capacity;
    int front;
    int rear;
} queue;

/* Initialize a queue with given capacity */
queue *init(int capacity) {
    queue *q = (queue *)malloc(sizeof(queue));

    if (q) {
        /* Allocate array for queue elements */
        q->arr = (int *)malloc(capacity * sizeof(int));
        q->capacity = capacity;
        q->front = -1;
        q->rear = 0;
    }

    return q;
}

/* Release memory allocated for queue */
void release(queue *q) {
    if (q->arr)
        free(q->arr);
    free(q);
}

/* Push an element into the queue */
bool push(queue *q, int n) {
    if (q->rear == q->capacity)
        return false;

    q->arr[q->rear] = n;
    q->rear++;

    return true;
}

/* Pop an element from the queue */
bool pop(queue *q, int *n) {
    if (q->front == q->rear - 1)
        return false;

    q->front++;
    *n = q->arr[q->front];

    return true;
}

/*
 * Determine if all courses can be finished
 * Algorithm: Topological Sort using BFS (Kahn's Algorithm)
 * - Build graph and in-degree array
 * - Enqueue courses with zero in-degree
 * - Remove nodes while updating in-degrees
 */
bool canFinish(int numCourses, int** prerequisites,
               int prerequisitesSize, int* prerequisitesColSize) {

    /* Store in-degree of each course */
    int *in_degree = (int *)calloc(numCourses, sizeof(int));
    /* Adjacency list representation of graph */
    int **graph = (int **)malloc(numCourses * sizeof(int *));
    /* Number of neighbors for each course */
    int *graph_size = (int *)calloc(numCourses, sizeof(int));
    /* Queue for BFS traversal */
    queue *q = init(numCourses);
    int finished = 0;

    /* Allocate adjacency list space */
    for (int i = 0; i < numCourses; i++)
        graph[i] = (int *)malloc(numCourses * sizeof(int));

    /* Build graph and compute in-degrees */
    for (int i = 0; i < prerequisitesSize; i++) {
        int before = prerequisites[i][1];
        int after = prerequisites[i][0];
        int index = graph_size[before];

        graph[before][index] = after;
        graph_size[before]++;
        in_degree[after]++;
    }

    /* Enqueue all courses with zero in-degree */
    for (int i = 0; i < numCourses; i++) {
        if (in_degree[i] == 0)
            push(q, i);
    }

    /* Perform BFS-based topological sorting */
    while (q->front < q->rear - 1) {
        int course = -1;

        pop(q, &course);
        finished++;
        /* Reduce in-degree of neighboring courses */
        for (int i = 0; i < graph_size[course]; i++) {
            int next = graph[course][i];

            in_degree[next]--;
            if (in_degree[next] == 0)
                push(q, next);
        }
    }

    /* Free allocated memory */
    free(in_degree);
    for (int i = 0; i < numCourses; i++)
        free(graph[i]);
    free(graph);
    free(graph_size);
    release(q);

    /* If all courses are processed, no cycle exists */
    return (finished == numCourses);
}
```
