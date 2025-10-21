[345. Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string/description/)

```c
/* 345. Reverse Vowels of a String */

/* Reverse only the vowels in a string while keeping other characters in place */
char* reverseVowels(char* s) {
    int i = 0;                /* Left pointer */
    int j = strlen(s) - 1;    /* Right pointer */

    /* Two-pointer approach to swap vowels */
    while (i < j) {
        /* Move left pointer until it points to a vowel */
        if (tolower(s[i]) != 'a' && tolower(s[i]) != 'e' &&
            tolower(s[i]) != 'i' && tolower(s[i]) != 'o' &&
            tolower(s[i]) != 'u') {
            i++;
            continue;
        }

        /* Move right pointer until it points to a vowel */
        if (tolower(s[j]) != 'a' && tolower(s[j]) != 'e' &&
            tolower(s[j]) != 'i' && tolower(s[j]) != 'o' &&
            tolower(s[j]) != 'u') {
            j--;
            continue;
        }

        /* Swap the vowels using XOR swap */
        s[i] = s[i] ^ s[j];
        s[j] = s[i] ^ s[j];
        s[i] = s[i] ^ s[j];

        i++;
        j--;
    }

    return s;  /* Return the modified string */
}
```
