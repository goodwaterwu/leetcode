[200. Number of Islands](https://leetcode.com/problems/number-of-islands/description/)

```c
/* 200. Number of Islands */

/*
 * Depth-First Search helper function.
 * grid : 2D grid representing the map
 * m    : number of rows in the grid
 * n    : number of columns in the grid
 * i,j  : current cell coordinates
 *
 * This function marks all connected land cells ('1') starting
 * from (i, j) as visited by converting them to water ('0').
 */
void dfs(char** grid, int m, int n, int i, int j) {
    /* Check for out-of-bounds indices or non-land cells */
    if (i < 0 || i >= m || j < 0 || j >= n || grid[i][j] != '1')
        return;

    /* Mark the current land cell as visited */
    grid[i][j] = '0';

    /* Recursively visit all four adjacent directions */
    dfs(grid, m, n, i - 1, j); /* up */
    dfs(grid, m, n, i, j - 1); /* left */
    dfs(grid, m, n, i + 1, j); /* down */
    dfs(grid, m, n, i, j + 1); /* right */
}

/*
 * Count the number of islands in the grid.
 * An island is formed by connecting adjacent lands ('1') horizontally or vertically.
 */
int numIslands(char** grid, int gridSize, int* gridColSize) {
    /* Variable to count the total number of islands */
    int num = 0;

    /* Traverse each cell in the grid */
    for (int i = 0; i < gridSize; i++) {
        for (int j = 0; j < *gridColSize; j++) {
            /* If an unvisited land cell is found */
            if (grid[i][j] == '1') {
                /* Increment island count */
                num++;

                /* Use DFS to mark the entire island as visited */
                dfs(grid, gridSize, *gridColSize, i, j);
            }
        }
    }

    /* Return the total number of islands */
    return num;
}
```

```c
/* 200. Number of Islands */

/*
 * Stack structure used to simulate DFS iteratively.
 * arr      : 2D array storing coordinate pairs (row, column)
 * capacity : maximum number of elements the stack can hold
 * top      : index of the next free position (also represents stack size)
 */
typedef struct Stack {
    int **arr;
    int capacity;
    int top;
} stack;

/*
 * Initialize a stack with the given capacity.
 * Each stack element stores two integers representing grid coordinates.
 */
stack *init(int capacity) {
    stack *s = (stack *)malloc(sizeof(stack));

    if (s) {
        /* Allocate space for stack elements */
        s->arr = (int **)malloc(capacity * sizeof(int *));
        for (int i = 0; i < capacity; i++)
            s->arr[i] = (int *)malloc(2 * sizeof(int));

        s->capacity = capacity;
        s->top = 0;
    }

    return s;
}

/*
 * Free all memory associated with the stack.
 */
void release(stack *s) {
    if (s->arr) {
        for (int i = 0; i < s->capacity; i++) {
            if (s->arr[i])
                free(s->arr[i]);
        }
        free(s->arr);
    }
    free(s);
}

/*
 * Push a coordinate (i, j) onto the stack.
 * Returns false if the stack is full.
 */
bool push(stack *s, int i, int j) {
    if (s->top == s->capacity)
        return false;

    s->arr[s->top][0] = i;
    s->arr[s->top][1] = j;
    s->top++;

    return true;
}

/*
 * Pop the top coordinate from the stack.
 * The popped values are stored in i and j.
 * Returns false if the stack is empty.
 */
bool pop(stack *s, int *i, int *j) {
    if (s->top == 0)
        return false;

    s->top--;
    *i = s->arr[s->top][0];
    *j = s->arr[s->top][1];

    return true;
}

/*
 * Peek the top element of the stack without removing it.
 * Returns false if the stack is empty.
 */
bool peer(stack *s, int *i, int *j) {
    if (s->top == 0)
        return false;

    *i = s->arr[s->top - 1][0];
    *j = s->arr[s->top - 1][1];

    return true;
}

/*
 * Count the number of islands in the grid using an explicit stack.
 * An island is a group of connected '1's (land) horizontally or vertically.
 */
int numIslands(char** grid, int gridSize, int* gridColSize) {
    /* Counter for the number of islands */
    int num = 0;

    /* Stack size is at most the total number of cells */
    stack *s = init(gridSize * (*gridColSize));

    /* Traverse every cell in the grid */
    for (int i = 0; i < gridSize; i++) {
        for (int j = 0; j < *gridColSize; j++) {
            /* Skip water cells */
            if (grid[i][j] == '0')
                continue;

            /* Found a new island */
            num++;

            /* Start DFS from this cell */
            push(s, i, j);
            while (s->top > 0) {
                int m = 0;
                int n = 0;

                /* Get the next cell to process */
                pop(s, &m, &n);

                /* Process only unvisited land cells */
                if (grid[m][n] == '1') {
                    /* Mark the cell as visited */
                    grid[m][n] = '0';

                    /* Push all valid neighboring land cells */
                    if (m - 1 >= 0 && grid[m - 1][n] == '1')
                        push(s, m - 1, n);
                    if (n - 1 >= 0 && grid[m][n - 1] == '1')
                        push(s, m, n - 1);
                    if (m + 1 < gridSize && grid[m + 1][n] == '1')
                        push(s, m + 1, n);
                    if (n + 1 < *gridColSize && grid[m][n + 1] == '1')
                        push(s, m, n + 1);
                }
            }
        }
    }

    /* Release allocated stack memory */
    release(s);

    /* Return the total number of islands */
    return num;
}
```
