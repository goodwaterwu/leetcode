[211. Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/description/)

```c
/* 211. Design Add and Search Words Data Structure - Trie + DFS */

typedef struct PrefixTree {
    struct PrefixTree *children[26]; /* Pointers to child nodes for 'a' to 'z' */
    bool is_word;                    /* Indicates whether this node marks the end of a word */
} WordDictionary;

WordDictionary* wordDictionaryCreate() {
    /* Create and initialize a new WordDictionary (Trie root) */
    WordDictionary *obj = (WordDictionary *)calloc(1, sizeof(WordDictionary));

    return obj;
}

void wordDictionaryAddWord(WordDictionary* obj, char* word) {
    /* Insert a word into the Trie */
    WordDictionary *cur = obj;

    for (int i = 0; i < strlen(word); i++) {
        if (cur->children[word[i]-'a'] == NULL)
            cur->children[word[i]-'a'] = (WordDictionary *)calloc(1, sizeof(WordDictionary));

        cur = cur->children[word[i]-'a'];
    }

    cur->is_word = true; /* Mark the end of the word */
}

bool wordDictionarySearch(WordDictionary* obj, char* word) {
    /* Search a word in the Trie with support for '.' wildcard */
    WordDictionary *cur = obj;

    for (int i = 0; i < strlen(word); i++) {
        /* If '.' is encountered, try all possible child branches */
        if (word[i] == '.') {
            for (int j = 0; j < 26; j++) {
                if (cur->children[j]) {
                    if (wordDictionarySearch(cur->children[j], word + i + 1))
                        return true;
                }
            }

            return false;
        }

        /* If the required child does not exist, the word cannot match */
        if (cur->children[word[i]-'a'] == NULL)
            return false;

        cur = cur->children[word[i]-'a'];
    }

    /* Return true only if this node represents the end of a valid word */
    return cur->is_word;
}

void wordDictionaryFree(WordDictionary* obj) {
    /* Recursively free all Trie nodes */
    if (!obj)
        return;

    for (int i = 0; i < 26; i++)
        wordDictionaryFree(obj->children[i]);

    free(obj);
}

/**
 * Your WordDictionary struct will be instantiated and called as such:
 * WordDictionary* obj = wordDictionaryCreate();
 * wordDictionaryAddWord(obj, word);
 * bool param_2 = wordDictionarySearch(obj, word);
 * wordDictionaryFree(obj);
 */
```
