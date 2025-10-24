[278. First Bad Version](https://leetcode.com/problems/first-bad-version/description/)

```c
/* 278. First Bad Version */
/* The API isBadVersion is defined for you. */
/* bool isBadVersion(int version); */

/* Use binary search to find the first bad version */
int firstBadVersion(int n) {
    int i = 1;        /* Start of the search range */
    int j = n;        /* End of the search range */
    int first = j;    /* Variable to store the first bad version */

    while (i <= j) {
        int m = i + (j - i) / 2; /* Prevent overflow */

        if (isBadVersion(m)) {
            first = m;  /* Update first bad version */
            j = m - 1;  /* Continue searching the left half */
        } else {
            i = m + 1;  /* Continue searching the right half */
        }
    }

    return first; /* Return the first bad version found */
}
```
