[190. Reverse Bits](https://leetcode.com/problems/reverse-bits/description/)

```c
/* 190. Reverse Bits */
int reverseBits(int n) {
    /* Variable to store the reversed result */
    int ret = 0;

    /* Iterate through all 32 bits of the integer */
    for (int i = 0; i < 32; i++) {
        /* Extract the i-th bit from n */
        int bit = (n >> i) & 1;

        /* Place the extracted bit at the reversed position */
        ret |= (bit << (31 - i));
    }

    /* Return the integer with all bits reversed */
    return ret;
}
```
