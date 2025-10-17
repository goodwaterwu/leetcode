[169. Majority Element](https://leetcode.com/problems/majority-element/description/)

```c
/* 169. Majority Element */

/* Find the element that appears more than ⌊n / 2⌋ times in the array using the Boyer-Moore Voting Algorithm */
int majorityElement(int* nums, int numsSize) {
    int i = 0;                  /* Iterator for traversing the array */
    int count = 0;              /* Counter for tracking candidate frequency balance */
    int candidate = nums[0];    /* Potential majority element */

    /* If only one element, return it directly */
    if (numsSize == 1) {
        return nums[0];
    }

    /* Traverse the array */
    while (i < numsSize) {
        /* Reset candidate when count drops to zero */
        if (count == 0)
            candidate = nums[i];

        /* Increment or decrement count depending on match */
        if (nums[i] == candidate)
            count++;
        else
            count--;

        i++;
    }

    /* The candidate after the loop is the majority element */
    return candidate;
}
```
