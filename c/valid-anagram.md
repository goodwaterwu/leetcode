[242. Valid Anagram](https://leetcode.com/problems/valid-anagram/description/)

```c
/* 242. Valid Anagram */

bool isAnagram(char* s, char* t) {
    /* Array to store frequency difference for each letter */
    int letters[26] = {0};
    /* Get the length of string s */
    int len = strlen(s);

    /* If lengths differ, they cannot be anagrams */
    if (len != strlen(t))
        return false;

    /* Count letters in s and t simultaneously */
    for (int i = 0; i < len; i++) {
        /* Increment count for s[i] */
        letters[s[i] - 'a']++;
        /* Decrement count for t[i] */
        letters[t[i] - 'a']--;
    }

    /* Check if all counts are zero */
    for (int i = 0; i < 26; i++) {
        /* If any count is not zero, strings are not anagrams */
        if (letters[i] != 0)
            return false;
    }

    /* All counts are zero, strings are anagrams */
    return true;
}
```
