[152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/description/)

```c
/* 152. Maximum Product Subarray */

/* Bottom-Up tabulation */

#define max(a, b) (((a) > (b)) ? (a) : (b))
#define min(a, b) (((a) < (b)) ? (a) : (b))

int maxProduct(int* nums, int numsSize) {
    int *dp1 = (int *)malloc(numsSize * sizeof(int));  /* dp1[i] = max product ending at index i */
    int *dp2 = (int *)malloc(numsSize * sizeof(int));  /* dp2[i] = min product ending at index i */
    int max_product = nums[0];                         /* Tracks the overall maximum product */

    dp1[0] = nums[0];  /* Initialize first element */
    dp2[0] = nums[0];

    for (int i = 1; i != numsSize; i++) {
        dp1[i] = max(max(dp1[i - 1] * nums[i], dp2[i - 1] * nums[i]), nums[i]);  /* Max product ending at i */
        dp2[i] = min(min(dp1[i - 1] * nums[i], dp2[i - 1] * nums[i]), nums[i]);  /* Min product ending at i */
        if (dp1[i] > max_product)
            max_product = dp1[i];  /* Update overall maximum */
    }

    free(dp1);
    free(dp2);

    return max_product;  /* Return the maximum product subarray */
}
```

```c
/* 152. Maximum Product Subarray */

/* Bottom-Up constant space */

#define max(a, b) (((a) > (b)) ? (a) : (b))
#define min(a, b) (((a) < (b)) ? (a) : (b))

int maxProduct(int* nums, int numsSize) {
    int prev_max = nums[0];  /* Tracks maximum product ending at previous index */
    int prev_min = nums[0];  /* Tracks minimum product ending at previous index */
    int curr_max = 0;        /* Current maximum product ending at index i */
    int curr_min = 0;        /* Current minimum product ending at index i */
    int max_product = nums[0];  /* Tracks overall maximum product */

    for (int i = 1; i != numsSize; i++) {
        curr_max = max(max(prev_max * nums[i], prev_min * nums[i]), nums[i]);  /* Max product ending at i */
        curr_min = min(min(prev_max * nums[i], prev_min * nums[i]), nums[i]);  /* Min product ending at i */
        if (curr_max > max_product)
            max_product = curr_max;  /* Update global maximum if needed */
        prev_max = curr_max;  /* Update previous maximum for next iteration */
        prev_min = curr_min;  /* Update previous minimum for next iteration */
    }

    return max_product;  /* Return the maximum product subarray */
}
```
