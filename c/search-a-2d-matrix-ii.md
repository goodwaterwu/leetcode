[240. Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/description/)

```c
/* 240. Search a 2D Matrix II */
/* Write an efficient algorithm that searches for a target value in an m x n
   integer matrix. The matrix has the following properties:
   - Integers in each row are sorted in ascending order from left to right.
   - Integers in each column are sorted in ascending order from top to bottom. */

bool searchMatrix(int** matrix, int matrixSize, int* matrixColSize, int target) {
    int i = 0;                      /* Start from the top-right corner */
    int j = *matrixColSize - 1;     /* Last column index */

    /* Move left if current element is greater than target,
       move down if current element is smaller than target */
    while (i < matrixSize && j >= 0) {
        if (matrix[i][j] > target)
            j--;                    /* Move left */
        else if (matrix[i][j] < target)
            i++;                    /* Move down */
        else
            return true;            /* Found the target */
    }

    return false;                   /* Target not found */
}
```
