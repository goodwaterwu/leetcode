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

```
/* 278. First Bad Version - Binary Search */

/* The API isBadVersion is defined for you. */
/* bool isBadVersion(int version); */

int firstBadVersion(int n) {
    int i = 1;            /* Left boundary of binary search */
    int j = n;            /* Right boundary of binary search */

    /* Perform binary search to locate the first bad version */
    while (i <= j) {
        /* Compute middle index safely to avoid integer overflow */
        int middle = i + (j - i) / 2;

        /* If middle version is bad, the first bad version is on the left side */
        if (isBadVersion(middle))
            j = middle - 1;
        /* Otherwise, the first bad version is on the right side */
        else
            i = middle + 1;
    }

    /* At the end of the loop, i points to the first bad version */
    return i;
}
```c
