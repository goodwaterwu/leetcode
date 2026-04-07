[208. Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/description/)

```c
/* 208. Implement Trie (Prefix Tree) - Trie Data Structure */

typedef struct PrefixTree {
    struct PrefixTree *children[26]; /* Pointers to child nodes for 'a' to 'z' */
    bool is_word;                    /* Indicates whether this node marks the end of a word */
} Trie;

Trie* trieCreate() {
    /* Create and initialize a new Trie node */
    Trie *obj = (Trie *)calloc(1, sizeof(Trie));
    return obj;
}

void trieInsert(Trie* obj, char* word) {
    /* Insert a word into the Trie */
    Trie *cur = obj;

    for (int i = 0; i < strlen(word); i++) {
        int idx = word[i] - 'a';

        if (cur->children[idx] == NULL)
            cur->children[idx] = (Trie *)calloc(1, sizeof(Trie));

        cur = cur->children[idx];
    }

    cur->is_word = true;
}

bool trieSearch(Trie* obj, char* word) {
    /* Return true if the word exists in the Trie */
    Trie *cur = obj;

    for (int i = 0; i < strlen(word); i++) {
        int idx = word[i] - 'a';

        if (cur->children[idx] == NULL)
            return false;

        cur = cur->children[idx];
    }

    return cur->is_word;
}

bool trieStartsWith(Trie* obj, char* prefix) {
    /* Return true if there exists a word starting with the given prefix */
    Trie *cur = obj;

    for (int i = 0; i < strlen(prefix); i++) {
        int idx = prefix[i] - 'a';

        if (cur->children[idx] == NULL)
            return false;

        cur = cur->children[idx];
    }

    return true;
}

void trieFree(Trie* obj) {
    /* Recursively free all Trie nodes */
    if (!obj)
        return;

    for (int i = 0; i < 26; i++)
        trieFree(obj->children[i]);

    free(obj);
}

/**
 * Your Trie struct will be instantiated and called as such:
 * Trie* obj = trieCreate();
 * trieInsert(obj, word);
 * bool param_2 = trieSearch(obj, word);
 * bool param_3 = trieStartsWith(obj, prefix);
 * trieFree(obj);
 */
```
