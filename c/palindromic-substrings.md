[647. Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/description/)

```c
/* 647. Palindromic Substrings */
int countPalindromes(char *s, int i, int j) {
    /* Variable to count palindromic substrings expanded from the center */
    int count = 0;

    /* Expand around the center while indices are valid and characters match */
    while (i >= 0 && j < strlen(s) && s[i] == s[j]) {
        /* A valid palindrome is found */
        count++;
        i--;
        j++;
    }

    /* Return the number of palindromes found for this center */
    return count;
}

int countSubstrings(char* s) {
    /* Variable to store the total number of palindromic substrings */
    int count = 0;

    /* Iterate through each character as a potential palindrome center */
    for (int i = 0; i < strlen(s); i++) {
        /* Count odd-length palindromes centered at i */
        count += countPalindromes(s, i, i);

        /* Count even-length palindromes centered between i and i + 1 */
        count += countPalindromes(s, i, i + 1);
    }

    /* Return the total count of palindromic substrings */
    return count;
}
```
