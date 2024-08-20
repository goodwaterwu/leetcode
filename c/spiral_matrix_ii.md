[Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii/)

```c
/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
int **generateMatrix(int n, int *returnSize, int **returnColumnSizes) {
    int **arr = NULL;
    int row_start = 0;
    int row_end = n - 1;
    int col_start = 0;
    int col_end = n - 1;
    int count = 1;

    arr = (int **)malloc(n * sizeof(int *));
    for (int i = 0; i != n; i++)
        arr[i] = (int *)malloc(n * sizeof(int));

    *returnSize = n;
    *returnColumnSizes = (int *)malloc(n * sizeof(int));
    for (int i = 0; i != n; i++)
        (*returnColumnSizes)[i] = n;

    while (row_start <= row_end && col_start <= col_end) {
	/* The last number in the center */
        if (row_start == row_end)
            arr[row_start][col_start] = count++;

	/* Fill top numbers(left to right) */
        for (int col = col_start; col < col_end; col++)
            arr[row_start][col] = count++;

	/* Fill right numbers(top to bottom) */
        for (int row = row_start; row < row_end; row++)
            arr[row][col_end] = count++;

	/* Fill bottom numbers(right to left) */
        for (int col = col_end; col > col_start; col--)
            arr[row_end][col] = count++;

	/* Fill left numbers(bottom to top) */
        for (int row = row_end; row > row_start; row--)
            arr[row][col_start] = count++;

        row_start++;
        row_end--;
        col_start++;
        col_end--;
    }

    return arr;
}
```
