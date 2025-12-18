[191. Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/description/)

```c
/* 191. Number of 1 Bits */
int hammingWeight(int n) {
    /* Variable to count the number of set bits (1s) */
    int weight = 0;

    /* Iterate through all 32 bits of the integer */
    for (int i = 0; i < 32; i++) {
        /* Check if the i-th bit is set */
        if ((n >> i) & 0x1)
            weight++;
    }

    /* Return the total count of set bits */
    return weight;
}
```
