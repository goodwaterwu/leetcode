[14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/description/)

```c
char* longestCommonPrefix(char** strs, int strsSize) {
    int j = 0;  /* Character index within each string */

    /* Iterate through each character position of the first string */
    while (strs[0][j]) {
        /* Compare the j-th character of every string */
        for (int i = 0; i != strsSize; i++) {
            /* If any string ends or its j-th character differs from strs[0][j],
               return the prefix up to (but not including) position j */
            if (strs[0][j] != strs[i][j])
                return strndup(strs[0], j);
        }
        j++;  /* Move to the next character position */
    }

    /* All characters matched up to the end of strs[0];
       return a copy of the entire first string */
    return strndup(strs[0], j);
}

```
