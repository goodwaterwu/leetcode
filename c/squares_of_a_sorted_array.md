[Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int *sortedSquares(int *nums, int numsSize, int *returnSize) {
    int left = 0;
    int right = numsSize - 1;
    int *ret = (int *)malloc(sizeof(int) * numsSize);

    if (!ret) {
        *returnSize = 0;
        return NULL;
    }

    *returnSize = numsSize;
    for (int i = numsSize - 1; i >= 0; i--) {
        int left_square = nums[left] * nums[left];
        int right_square = nums[right] * nums[right];

        /* Set the bigger square numbers to result */
        if (left_square > right_square) {
            ret[i] = left_square;
            left++;
        } else {
            ret[i] = right_square;
            right--;
        }
    }

    return ret;
}
```
