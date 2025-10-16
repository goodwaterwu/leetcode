[344. Reverse String](https://leetcode.com/problems/reverse-string/description/)

```c
/* 344. Reverse String */
void reverseString(char* s, int sSize) {
    int i = 0;              /* Initialize the left index */
    int j = sSize - 1;      /* Initialize the right index */

    /* Continue swapping characters until the two indices meet */
    while (i < j) {
        /* Swap s[i] and s[j] using XOR (without a temporary variable) */
        s[i] = s[i] ^ s[j];
        s[j] = s[i] ^ s[j];
        s[i] = s[i] ^ s[j];

        i++;    /* Move the left index to the right */
        j--;    /* Move the right index to the left */
    }
}
```
