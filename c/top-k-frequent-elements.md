[347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/description/)

```c
/* 347. Top K Frequent Elements */
/* Given an integer array nums and an integer k, return the k most frequent elements.
   The result can be returned in any order. */

typedef struct Dictionary {
    int key;     /* The number from nums */
    int value;   /* Its frequency */
} dict;

/* Comparison function for qsort: sort integers in ascending order */
int compare1(const void *a, const void *b) {
    return (*(int *)a - *(int *)b);
}

/* Comparison function for qsort: sort dict structs by value in descending order */
int compare2(const void *a, const void *b) {
    return ((*(dict *)b).value - (*(dict *)a).value);
}

/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* topKFrequent(int* nums, int numsSize, int k, int* returnSize) {
    dict *d = (dict *)malloc(numsSize * sizeof(dict)); /* Array to store unique numbers and frequencies */
    int *arr = (int *)malloc(k * sizeof(int));         /* Result array */
    int i = 0;
    int j = 1;

    *returnSize = k;

    qsort(nums, numsSize, sizeof(int), compare1); /* Sort nums to count frequencies easily */
    d[i].key = nums[0];
    d[i].value = 1;
    i++;

    /* Count frequency of each unique number */
    while (j < numsSize) {
        if (nums[j] == d[i - 1].key) {
            d[i - 1].value++;
        } else {
            d[i].key = nums[j];
            d[i].value = 1;
            i++;
        }
        j++;
    }

    qsort(d, i, sizeof(dict), compare2); /* Sort dict by frequency descending */

    /* Take the top k keys */
    for (int l = 0; l != k; l++)
        arr[l] = d[l].key;

    return arr;
}
```
