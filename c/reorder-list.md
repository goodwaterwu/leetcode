[143. Reorder List](https://leetcode.com/problems/reorder-list/description/)

```c
/* 143. Reorder List */
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
void reorderList(struct ListNode* head) {
    /* Pointers used to find the middle of the linked list */
    struct ListNode *p = head;
    struct ListNode *q = head;

    /* Pointers used to reverse the second half of the list */
    struct ListNode *prev = NULL;
    struct ListNode *curr = NULL;
    struct ListNode *post = NULL;

    /* Flag to alternate between nodes from the first and second halves */
    bool first = true;

    /* Find the middle of the list using slow and fast pointers */
    while (q && q->next) {
        p = p->next;
        q = q->next->next;
    }

    /* Reverse the second half of the list starting from the middle */
    prev = NULL;
    curr = p;
    while (curr) {
        post = curr->next;
        curr->next = prev;
        prev = curr;
        curr = post;
    }

    /* Merge the first half and the reversed second half alternately */
    curr = head;
    p = head->next;
    q = prev;
    while (p && q) {
        struct ListNode *node = NULL;

        /* Alternate linking nodes from the second and first halves */
        if (first) {
            curr->next = q;
            q = q->next;
        } else {
            curr->next = p;
            p = p->next;
        }

        curr = curr->next;
        first = !first;
    }
}
```
