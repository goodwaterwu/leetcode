[383. Ransom Note](https://leetcode.com/problems/ransom-note/description/)

```c
/* 383. Ransom Note - Hash Table (Character Frequency Counting) */

bool canConstruct(char* ransomNote, char* magazine) {
    /* Frequency array to count occurrences of each lowercase letter */
    int letters[26] = {0};

    /* Count each character in magazine */
    while (*magazine != '\0') {
        letters[*magazine - 'a']++;
        magazine++;
    }

    /* Check if ransomNote can be formed using counted letters */
    while (*ransomNote != '\0') {
        letters[*ransomNote - 'a']--;

        /* If any character count becomes negative, construction is impossible */
        if (letters[*ransomNote - 'a'] < 0)
            return false;

        ransomNote++;
    }

    /* All characters are available in sufficient quantity */
    return true;
}
```
