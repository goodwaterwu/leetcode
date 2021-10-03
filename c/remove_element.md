[Remove Element](https://leetcode.com/problems/remove-element/)

```c
int removeElement(int *nums, int numsSize, int val) {
    int index = 0; /* The new array index */

    /* i is the index to be removed or moved */
    for (int i = 0; i != numsSize; i++) {
        if (nums[i] != val)
            nums[index++] = nums[i];
    }

    return index;
}
```
