[48. Rotate Image](https://leetcode.com/problems/rotate-image/description/)

```c
/* 48. Rotate Image */
void swap(int *a, int *b) {
    /* Temporary variable to store one value during swap */
    int tmp = *a;

    /* Swap the values pointed to by a and b */
    *a = *b;
    *b = tmp;
}

void rotate(int** matrix, int matrixSize, int* matrixColSize) {
    /* First step: transpose the matrix (swap across the diagonal) */
    for (int i = 0; i < matrixSize; i++) {
        for (int j = i + 1; j < (*matrixColSize); j++)
            swap(&matrix[i][j], &matrix[j][i]);
    }

    /* Second step: reverse each row to achieve a 90-degree clockwise rotation */
    for (int i = 0; i < matrixSize; i++) {
        int j = 0;
        int k = (*matrixColSize) - 1;

        /* Swap elements symmetrically from left to right */
        while (j <= k) {
            swap(&matrix[i][j], &matrix[i][k]);
            j++;
            k--;
        }
    }
}
```
