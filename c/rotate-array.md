[189. Rotate Array](https://leetcode.com/problems/rotate-array/description/)

```c
/* 189. Rotate Array */

/* Swap two integers in place */
void swap(int *a, int *b) {
    int tmp = *a;
    *a = *b;
    *b = tmp;
}

/* Rotate an array to the right by k steps using in-place reversal */
void rotate(int* nums, int numsSize, int k) {
    int i = 0;
    int j = numsSize - 1;
    int new_k = k % numsSize;  /* Normalize k to avoid unnecessary rotations */

    /* Step 1: Reverse the entire array */
    while (i < j) {
        swap(&nums[i], &nums[j]);
        i++;
        j--;
    }

    /* Step 2: Reverse the first part (first new_k elements) */
    i = 0;
    j = new_k - 1;
    while (i < j) {
        swap(&nums[i], &nums[j]);
        i++;
        j--;
    }

    /* Step 3: Reverse the remaining part (from new_k to end) */
    i = new_k;
    j = numsSize - 1;
    while (i < j) {
        swap(&nums[i], &nums[j]);
        i++;
        j--;
    }
}
```
