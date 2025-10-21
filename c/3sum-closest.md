[16. 3Sum Closest](https://leetcode.com/problems/3sum-closest/description/)

```c
/* 16. 3Sum Closest */

int compare(const void* a, const void* b) {
    return (*(int *)a - *(int *)b);
}

/* Find the sum of three integers in nums that is closest to the target */
int threeSumClosest(int* nums, int numsSize, int target) {
    long long int closest = INT_MAX;  /* Initialize closest sum as a large value */

    qsort(nums, numsSize, sizeof(int), compare);  /* Sort the array for two-pointer approach */

    for (int i = 0; i != numsSize - 2; i++) {
        int j = i + 1;               /* Left pointer */
        int k = numsSize - 1;        /* Right pointer */

        /* Two-pointer search for sum closest to target */
        while (j < k) {
            long long int sum = nums[i] + nums[j] + nums[k];  /* Current triplet sum */

            /* Update closest if current sum is nearer to target */
            if (abs(target - sum) < abs(target - closest))
                closest = sum;

            /* Move pointers based on comparison with target */
            if (sum < target)
                j++;       /* Need a larger sum */
            else if (sum > target)
                k--;       /* Need a smaller sum */
            else
                return sum;  /* Exact match found */
        }
    }

    return closest;  /* Return the closest sum found */
}
```
