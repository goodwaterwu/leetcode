[242. Valid Anagram](https://leetcode.com/problems/valid-anagram/description/)

```c
/* 242. Valid Anagram */

bool isAnagram(char* s, char* t) {
    /* Array to track the frequency difference of each letter */
    int letters[26] = {0};
    /* Get length of string s */
    int len = strlen(s);

    /* If lengths are different, they cannot be anagrams */
    if (len != strlen(t))
        return false;

    /* Count frequency of each character in s */
    for (int i = 0; i < strlen(s); i++)
        letters[s[i] - 'a']++;

    /* Decrease frequency based on characters in t */
    for (int i = 0; i < strlen(t); i++)
        letters[t[i] - 'a']--;

    /* Check if all frequencies return to zero */
    for (int i = 0; i < 26; i++) {
        /* If any value is not zero, it's not an anagram */
        if (letters[i] != 0)
            return false;
    }

    /* All letter counts are balanced */
    return true;
}
```
