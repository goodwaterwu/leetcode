[56. Merge Intervals](https://leetcode.com/problems/merge-intervals/description/)

```c
/* 56. Merge Intervals */
/* Given an array of intervals where intervals[i] = [start_i, end_i],
   merge all overlapping intervals, and return an array of the non-overlapping
   intervals that cover all the intervals in the input. */

/* Comparator function used by qsort to sort intervals by their start value */
int compare(const void *a, const void *b) {
    int *itv1 = *(int **)a;                 /* Dereference and access first interval */
    int *itv2 = *(int **)b;                 /* Dereference and access second interval */
    return (itv1[0] - itv2[0]);             /* Sort by the start time of each interval */
}

/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
int** merge(int** intervals, int intervalsSize, int* intervalsColSize, int* returnSize, int** returnColumnSizes) {
    int **arr = (int **)malloc(intervalsSize * sizeof(int *)); /* Allocate space for merged intervals */
    int i = 1;                                                 /* Start merging from the second interval */

    *returnSize = 0;                                           /* Initialize merged count to 0 */
    *returnColumnSizes = (int *)malloc(intervalsSize * sizeof(int)); /* Each interval has 2 columns */

    /* Sort all intervals by their start value */
    qsort(intervals, intervalsSize, sizeof(int *), compare);

    /* Initialize first merged interval */
    arr[*returnSize] = (int *)malloc(2 * sizeof(int));
    arr[*returnSize][0] = intervals[0][0];
    arr[*returnSize][1] = intervals[0][1];
    (*returnColumnSizes)[0] = 2;
    (*returnSize)++;

    /* Traverse through all intervals to merge overlaps */
    while (i < intervalsSize) {
        /* If current interval overlaps with the previous merged one */
        if (intervals[i][0] <= arr[(*returnSize) - 1][1]) {
            /* Extend the end of the merged interval if needed */
            if (intervals[i][0] < arr[(*returnSize) - 1][0])
                arr[(*returnSize) - 1][0] = intervals[i][0];
            if (intervals[i][1] > arr[(*returnSize) - 1][1])
                arr[(*returnSize) - 1][1] = intervals[i][1];
        } else {
            /* No overlap — start a new interval */
            arr[*returnSize] = (int *)malloc(2 * sizeof(int));
            arr[*returnSize][0] = intervals[i][0];
            arr[*returnSize][1] = intervals[i][1];
            (*returnColumnSizes)[*returnSize] = 2;
            (*returnSize)++;
        }
        i++;
    }

    return arr;                                                /* Return merged intervals */
}
```
