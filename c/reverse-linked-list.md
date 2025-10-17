[206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/description/)

```c
/* 206. Reverse Linked List */

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */

/* Reverse a singly-linked list iteratively */
struct ListNode* reverseList(struct ListNode* head) {
    struct ListNode *prev = NULL;      /* Previous node, initially NULL */
    struct ListNode *current = head;   /* Current node starting from head */

    /* Iterate through the list */
    while (current) {
        struct ListNode *tmp = current->next;  /* Store next node */
        current->next = prev;                  /* Reverse the link */
        prev = current;                        /* Move prev forward */
        current = tmp;                         /* Move current forward */
    }

    return prev;  /* New head of the reversed list */
}
```
