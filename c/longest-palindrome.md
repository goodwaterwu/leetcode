[409. Longest Palindrome](https://leetcode.com/problems/longest-palindrome/description/)

```c
/* 409. Longest Palindrome - Greedy + Hash Table (Character Frequency Counting) */

int longestPalindrome(char* s) {
    /* Arrays to count frequencies of uppercase and lowercase letters */
    int upper[26] = {0};
    int lower[26] = {0};
    int longest = 0;   /* Stores the total length of the longest palindrome */
    bool odd = false; /* Indicates whether at least one odd-count character exists */

    /* Count the frequency of each character */
    while (*s != '\0') {
        if (isupper(*s))
            upper[*s - 'A']++;
        else
            lower[*s - 'a']++;
        s++;
    }

    /* Accumulate usable character counts to form the palindrome */
    for (int i = 0; i < 26; i++) {
        if (upper[i] > 0) {
            if (upper[i] % 2 == 0) {
                /* Even counts can be fully used */
                longest += upper[i];
            } else {
                /* Use the largest even part, keep one for possible center */
                longest = longest + upper[i] - 1;
                odd = true;
            }
        }

        if (lower[i] > 0) {
            if (lower[i] % 2 == 0) {
                /* Even counts can be fully used */
                longest += lower[i];
            } else {
                /* Use the largest even part, keep one for possible center */
                longest = longest + lower[i] - 1;
                odd = true;
            }
        }
    }

    /* If there is at least one odd-count character, place one in the center */
    return ((odd == true) ? (longest + 1) : longest);
}
```
