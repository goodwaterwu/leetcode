[Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>

#define MAX_ARRAY_SIZE 200

void merge(int* nums1, int nums1Size, int m, int* nums2, int nums2Size, int n)
{
    /* n == 0 means nums1 is the answer. */
    if (n == 0)
        return;

    /* m == 0 means nums1 should be the same as nums2. */
    if (m == 0) {
        memcpy(nums1, nums2, n * sizeof(int));
    } else {
        int new_nums[MAX_ARRAY_SIZE] = {0};
        int *dup_nums1 = nums1;
        int *dup_nums2 = nums2;

        for (int i = 0; i < m + n; i++) {
            if (*dup_nums1 <= *dup_nums2) {
                new_nums[i] = *dup_nums1;
                if (dup_nums1 + 1 - nums1 != m)
                    dup_nums1 = dup_nums1 + 1;
                else
                    *dup_nums1 = (int)pow(10.0, 9.0) + 1; /* This never adds to nums1. */
            } else {
                new_nums[i] = *dup_nums2;
                if (dup_nums2 + 1 - nums2 != n)
                    dup_nums2 = dup_nums2 + 1;
                else
                    *dup_nums2 = (int)pow(10.0, 9.0) + 1; /* This never adds to nums1. */
            }
        }

        memcpy(nums1, new_nums, (m + n) * sizeof(int));
    }
}
```
