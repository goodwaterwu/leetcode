[67. Add Binary](https://leetcode.com/problems/add-binary/description/)

```c
/* 67. Add Binary - String Manipulation + Simulation */

void swap(char *a, char *b) {
    /* Swap the values of two characters */
    char tmp = *a;

    *a = *b;
    *b = tmp;
}

void reverse(char *s) {
    /* Reverse a null-terminated string in place using two pointers */
    int i = 0;
    int j = strlen(s) - 1;

    while (i < j) {
        swap(&s[i], &s[j]);
        i++;
        j--;
    }
}

char* addBinary(char* a, char* b) {
    /* Perform binary addition by simulating bit-by-bit addition with carry */
    bool carry = false;
    int len_a = strlen(a);
    int len_b = strlen(b);
    int len = (len_a > len_b) ? len_a : len_b;
    int i = 0;
    int idx = 0;
    char *ret = (char *)calloc(len + 2, sizeof(char));

    /* Reverse both input strings to simplify addition from least significant bit */
    reverse(a);
    reverse(b);

    /* Add bits from both strings with carry handling */
    while (i < len) {
        char m = 0;
        char n = 0;

        /* If one string is shorter, treat missing bits as '0' */
        if (i >= len_a)
            m = '0';
        else
            m = a[i];

        if (i >= len_b)
            n = '0';
        else
            n = b[i];

        /* Binary addition logic with carry */
        if (carry) {
            if (m == '0' && n == '0') {
                ret[idx] = '1';
                carry = false;
            } else if (m == '1' && n == '1') {
                ret[idx] = '1';
            } else {
                ret[idx] = '0';
            }
        } else {
            if (m == '0' && n == '0') {
                ret[idx] = '0';
            } else if (m == '1' && n == '1') {
                ret[idx] = '0';
                carry = true;
            } else {
                ret[idx] = '1';
            }
        }
        i++;
        idx++;
    }

    /* If carry remains, append it as the most significant bit */
    if (carry)
        ret[idx] = '1';

    /* Reverse the result to restore correct bit order */
    reverse(ret);

    return ret;
}
```
