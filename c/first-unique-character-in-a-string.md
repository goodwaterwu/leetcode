[387. First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/description/)

```c
/* 387. First Unique Character in a String */
int firstUniqChar(char* s) {
    int count[26] = {0};  /* Array to store the frequency of each lowercase letter */
    int i = 0;            /* Index for iterating through the string */

    /* Count the frequency of each character in the string */
    while (s[i]) {
        count[s[i] - 'a']++;
        i++;
    }

    i = 0;  /* Reset index to find the first unique character */

    /* Iterate through the string to find the first character with count 1 */
    while (s[i]) {
        if (count[s[i] - 'a'] == 1)
            return i;  /* Return the index of the first unique character */
        i++;
    }

    /* If no unique character is found, return -1 */
    return -1;
}

```
