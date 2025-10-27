[378. Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/description/)

```c
/* 378. Kth Smallest Element in a Sorted Matrix */
/* Given an n x n matrix where each of the rows and columns is sorted in ascending order,
   return the kth smallest element in the matrix. */

int countSmallerEqual(int **matrix, int rowSize, int colSize, int target)
{
    int row = 0;             /* Start from top-right corner */
    int col = colSize - 1;
    int count = 0;           /* Count of numbers ≤ target */

    while (row < rowSize && col >= 0) {
        if (matrix[row][col] > target) {
            col--;           /* Move left if current element > target */
        } else {
            count += col + 1;/* All elements in this row up to 'col' are ≤ target */
            row++;           /* Move to next row */
        }
    }

    return count;
}

int kthSmallest(int** matrix, int matrixSize, int* matrixColSize, int k) {
    int i = matrix[0][0];                                  /* Minimum element */
    int j = matrix[matrixSize - 1][*matrixColSize - 1];    /* Maximum element */

    /* Binary search on the value range */
    while (i < j) {
        int m = i + (j - i) / 2;
        int count = countSmallerEqual(matrix, matrixSize, *matrixColSize, m);

        if (count < k) {      /* If there are fewer than k elements ≤ m */
            i = m + 1;        /* Search in the larger half */
        } else {
            j = m;            /* Otherwise search in the smaller half */
        }
    }

    return i;                 /* i (or j) will be the kth smallest element */
}
```
