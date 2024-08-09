[Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

```c
int searchLeftBorder(int *nums, int numsSize, int target)
{
    int low = 0;
    int high = numsSize - 1;
    int left = -1;

    while (low <= high) {
        int middle = low + (high - low) / 2;

        if (nums[middle] == target) {
            left = middle; /* Suppose the left bound equals middle */
            high = middle - 1; /* Search the left part to get the leftest bound */
        } else if (nums[middle] < target) {
            low = middle + 1; /* Search the right part */
        } else {
            high = middle - 1; /* Search the left part */
        }
    }

    return left;
}

int searchRightBorder(int *nums, int numsSize, int target)
{
    int low = 0;
    int high = numsSize - 1;
    int right = -1;

    while (low <= high) {
        int middle = low + (high - low) / 2;

        if (nums[middle] == target) {
            right = middle; /* Suppose the right bound equals middle */
            low = middle + 1; /* Search the right part to get the rightest bound */
        } else if (nums[middle] < target) {
            low = middle + 1; /* Search the right part */
        } else {
            high = middle - 1; /* Search the left part */
        }
    }

    return right;
}

/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int *searchRange(int *nums, int numsSize, int target, int *returnSize) {
    int *range = (int *)malloc(sizeof(int) * 2);

    if (!range) {
        *returnSize = 0;
        return NULL;
    }

    *returnSize = 2;
    range[0] = searchLeftBorder(nums, numsSize, target);
    range[1] = searchRightBorder(nums, numsSize, target);

    return range;
}
```
