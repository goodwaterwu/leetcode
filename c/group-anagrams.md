[49. Group Anagrams](https://leetcode.com/problems/group-anagrams/description/)

```c
/* 49. Group Anagrams */

typedef struct Hash {
    char *key;      /* Sorted version of the string */
    char *value;    /* Original string */
} hash;

/* Compare two characters for qsort */
int compare(const void *a, const void *b) {
    return (*(char *)a - *(char *)b);
}

/* Compare hash structs by their sorted key */
int compare_hash(const void *a, const void *b) {
    hash *h1 = (hash *)a;
    hash *h2 = (hash *)b;

    return (strcmp(h1->key, h2->key));
}

/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
char*** groupAnagrams(char** strs, int strsSize, int* returnSize, int** returnColumnSizes) {
    /* groups will store all grouped anagrams */
    char ***groups = (char ***)malloc(strsSize * sizeof(char **));

    /* m = number of groups, n = number of strings inside current group */
    int m = 0;
    int n = 0;

    /* Initial capacity for each group's inner array */
    int capacity = 2;

    /* Copy of sorted strings */
    char **copy = (char **)calloc(strsSize, sizeof(char *));

    /* Hash array storing sorted key + original value */
    hash *h = (hash *)calloc(strsSize, sizeof(hash));
    hash *tmp = h;  /* Not used, but kept since original code has it */

    /* Step 1: Create (sorted_string, original_string) pairs */
    for (int i = 0; i < strsSize; i++) {
        copy[i] = (char *)calloc(101, sizeof(char));
        strncpy(copy[i], strs[i], strlen(strs[i]));
        qsort(copy[i], strlen(strs[i]), sizeof(char), compare);

        h[i].key = copy[i];
        h[i].value = strs[i];
    }

    /* Step 2: Sort hash array based on sorted string key */
    qsort(h, strsSize, sizeof(hash), compare_hash);

    /* Allocate column size array */
    *returnColumnSizes = (int *)calloc(strsSize, sizeof(int));
    *returnSize = 0;

    /* Step 3: Start the first group */
    groups[m] = (char **)calloc(strsSize, sizeof(char **));
    (*returnSize)++;

    groups[m][n] = h[0].value;
    (*returnColumnSizes)[m]++;
    n++;

    /* Step 4: Group by comparing sorted keys */
    for (int i = 1; i < strsSize; i++) {
        /* If new key differs, start a new group */
        if (strcmp(h[i].key, h[i - 1].key)) {
            m++;
            groups[m] = (char **)calloc(capacity, sizeof(char **));
            (*returnSize)++;
            n = 0;
            capacity = 2;
        }

        /* Add string to current group */
        groups[m][n] = h[i].value;
        (*returnColumnSizes)[m]++;
        n++;

        /* Expand inner array if needed */
        if (n >= capacity) {
            capacity *= 2;
            groups[m] = (char **)realloc(groups[m], capacity * sizeof(char **));
        }
    }

    return groups;
}
```
