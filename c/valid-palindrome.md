[125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/description/)

```c
/* 125. Valid Palindrome */
bool isPalindrome(char* s) {
    int i = 0;              /* Left pointer starting from the beginning */
    int j = strlen(s) - 1;  /* Right pointer starting from the end */

    /* Continue checking characters while left pointer <= right pointer */
    while (i <= j) {
        /* Skip non-alphanumeric characters from the left side */
        if (!isalnum(s[i])) {
            i++;
            continue;
        }

        /* Skip non-alphanumeric characters from the right side */
        if (!isalnum(s[j])) {
            j--;
            continue;
        }

        /* Compare the lowercase form of both characters */
        if (tolower(s[i]) != tolower(s[j]))
            return false;   /* Not a palindrome */

        /* Move both pointers toward the center */
        i++;
        j--;
    }

    /* All matched: the string is a palindrome */
    return true;
}
```
