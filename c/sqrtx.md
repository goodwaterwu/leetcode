[69. Sqrt(x)](https://leetcode.com/problems/sqrtx/description/)

```c
/* 69. Sqrt(x) */
/* Given a non-negative integer x, return the square root of x rounded down to the nearest integer.
   The returned integer should be the largest integer such that (integer * integer) <= x. */

int mySqrt(int x) {
    int i = 0;           /* Start of binary search range */
    int j = x;           /* End of binary search range */
    int candidate = 0;   /* Stores the closest integer square root found */

    while (i <= j) {
        long long int m = i + (j - i) / 2; /* Middle point, use long long to prevent overflow */

        if (m * m > x) {
            j = m - 1;   /* If square too large, search in the left half */
        } else if (m * m < x) {
            candidate = m; /* Update candidate */
            i = m + 1;     /* Search in the right half */
        } else {
            return m;     /* Found exact square root */
        }
    }

    /* Return the floor value of sqrt(x) */
    return candidate;
}
```
