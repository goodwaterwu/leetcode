[57. Insert Interval](https://leetcode.com/problems/insert-interval/description/)

```c
/* 57. Insert Interval - Greedy + Interval Merging */

#define min(a, b) (((a) < (b)) ? (a) : (b))
#define max(a, b) (((a) > (b)) ? (a) : (b))

/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
int** insert(int** intervals, int intervalsSize, int* intervalsColSize, int* newInterval, int newIntervalSize, int* returnSize, int** returnColumnSizes) {
    /* Allocate space for the worst case: intervalsSize + 1 intervals */
    int **ret = (int **)malloc((intervalsSize + 1) * sizeof(int *));
    int idx = 0;        /* Index for constructing the result array */
    bool first = false;/* Indicates whether the new interval has already been inserted */

    /* Initialize return size and column sizes */
    *returnSize = intervalsSize + 1;
    *returnColumnSizes = (int *)malloc((intervalsSize + 1) * sizeof(int));
    for (int i = 0; i < intervalsSize + 1; i++) {
        ret[i] = (int *)calloc(2, sizeof(int));
        (*returnColumnSizes)[i] = 2;
    }

    /* Special case: no existing intervals */
    if (intervalsSize == 0) {
        ret[0][0] = newInterval[0];
        ret[0][1] = newInterval[1];
        return ret;
    }

    /* Traverse existing intervals and merge or insert accordingly */
    for (int i = 0; i < intervalsSize; i++) {
        if (newInterval[1] < intervals[i][0]) {
            /* New interval comes completely before the current interval */
            ret[idx][0] = newInterval[0];
            ret[idx][1] = newInterval[1];
            idx++;

            /* Copy the remaining intervals */
            for (int j = i; j < intervalsSize; j++) {
                ret[idx][0] = intervals[j][0];
                ret[idx][1] = intervals[j][1];
                idx++;
            }

            first = true;
            break;
        } else if (newInterval[0] > intervals[i][1]) {
            /* Current interval comes completely before the new interval */
            ret[idx][0] = intervals[i][0];
            ret[idx][1] = intervals[i][1];
            idx++;
        } else {
            /* Overlapping intervals: merge them by expanding newInterval */
            newInterval[0] = min(newInterval[0], intervals[i][0]);
            newInterval[1] = max(newInterval[1], intervals[i][1]);
        }
    }

    /* If newInterval has not been inserted yet, append it at the end */
    if (!first) {
        ret[idx][0] = newInterval[0];
        ret[idx][1] = newInterval[1];
        idx++;
    }

    /* Shrink allocated memory to the actual result size */
    *returnSize = idx;
    ret = realloc(ret, idx * sizeof(int *));
    *returnColumnSizes = realloc(*returnColumnSizes, idx * sizeof(int));

    return ret;
}
```
