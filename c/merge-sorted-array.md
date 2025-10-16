[88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/description/)

```c
/* 88. Merge Sorted Array */
void merge(int* nums1, int nums1Size, int m, int* nums2, int nums2Size, int n) {
    /* i: index for the last position in the merged array */
    /* j: index for the last element in the initial part of nums1 */
    /* k: index for the last element in nums2 */
    int i = m + n - 1;
    int j = m - 1;
    int k = n - 1;

    /* Merge nums1 and nums2 from the end to the beginning */
    while (j >= 0 && k >= 0) {
        /* Compare the last elements of nums1 and nums2 */
        /* Place the larger one at the end of nums1 */
        if (nums1[j] > nums2[k]) {
            nums1[i] = nums1[j];
            j--;
        } else {
            nums1[i] = nums2[k];
            k--;
        }
        i--;
    }

    /* Copy remaining elements from nums1 (if any) */
    /* (This loop usually does nothing because nums1’s elements are already in place) */
    while (j >= 0) {
        nums1[i] = nums1[j];
        i--;
        j--;
    }

    /* Copy remaining elements from nums2 (if any) */
    /* (Needed when some smaller nums2 elements are left) */
    while (k >= 0) {
        nums1[i] = nums2[k];
        i--;
        k--;
    }
}
```
