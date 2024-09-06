[Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int *spiralOrder(int **matrix, int matrixSize, int *matrixColSize, int *returnSize) {
    int *arr = NULL;
    int row_start = 0;
    int row_end = matrixSize - 1;
    int col_start = 0;
    int col_end = *matrixColSize - 1;
    int size = matrixSize * *matrixColSize;
    int count = 0;

    arr = (int *)malloc(sizeof(int) * size);
    if (!arr)
        return NULL;

    *returnSize = size;
    while (1) {
        for (int col = col_start; col <= col_end; col++)
            arr[count++] = matrix[row_start][col];

        if (count >= size)
            break;
        
        row_start++;
        for (int row = row_start; row <= row_end; row++)
            arr[count++] = matrix[row][col_end];

        if (count >= size)
            break;

        col_end--;
        for (int col = col_end; col >= col_start; col--)
            arr[count++] = matrix[row_end][col];

        if (count >= size)
            break;

        row_end--;
        for (int row = row_end; row >= row_start; row--)
            arr[count++] = matrix[row][col_start];

        if (count >= size)
            break;

        col_start++;
    }

    return arr;
}
```
