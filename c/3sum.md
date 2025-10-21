[15. 3Sum](https://leetcode.com/problems/3sum/description/)

```c

/* 15. 3Sum */

int compare(const void *a, const void *b) {
    return (*(int *)a - *(int *)b);
}

/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
int** threeSum(int* nums, int numsSize, int* returnSize, int** returnColumnSizes) {
    int capacity = 1;  /* Initial capacity for the result array */
    int **arr = (int **)malloc(sizeof(int *));  /* Allocate memory for result array */
    *returnColumnSizes = (int *)malloc(sizeof(int));  /* Allocate memory for column sizes */

    qsort(nums, numsSize, sizeof(int), compare);  /* Sort the array for two-pointer approach */
    *returnSize = 0;  /* Initialize the number of triplets found */

    for (int i = 0; i != numsSize - 2; i++) {
        /* Skip duplicate elements to avoid duplicate triplets */
        if (i > 0 && nums[i] == nums[i - 1])
            continue;
        
        int j = i + 1;          /* Left pointer */
        int k = numsSize - 1;   /* Right pointer */

        /* Two-pointer search for pairs that sum with nums[i] to 0 */
        while (j < k) {
            int sum = nums[i] + nums[j] + nums[k];  /* Current triplet sum */

            /* Skip duplicates for left pointer */
            if (j > i + 1 && nums[j] == nums[j - 1]){
                j++;
            } 
            /* Skip duplicates for right pointer */
            else if (k < numsSize - 1 && nums[k] == nums[k + 1]) {
                k--;
            } 
            else {
                /* Move pointers based on sum comparison */
                if (sum < 0) {
                    j++;  /* Need a larger sum */
                } else if (sum > 0) {
                    k--;  /* Need a smaller sum */
                } else {
                    /* Found a valid triplet */
                    arr[*returnSize] = (int *)malloc(3 * sizeof(int));  /* Allocate memory for triplet */
                    (*returnColumnSizes)[*returnSize] = 3;  /* Each triplet has size 3 */
                    arr[*returnSize][0] = nums[i];
                    arr[*returnSize][1] = nums[j];
                    arr[*returnSize][2] = nums[k];
                    (*returnSize)++;

                    j++;  /* Move both pointers to search for next triplet */
                    k--;

                    /* Resize the result array if capacity exceeded */
                    if (*returnSize >= capacity) {
                        capacity = capacity * 2;  /* Double the capacity */
                        arr = (int **)realloc(arr, capacity * sizeof(int *));
                        *returnColumnSizes = (int *)realloc(*returnColumnSizes, capacity * sizeof(int));
                    }
                }
            }
        }
    }

    return arr;  /* Return the array of triplets */
}
```
