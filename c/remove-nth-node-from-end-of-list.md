[19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

```c
/* 19. Remove Nth Node From End of List */

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */

/* Remove the Nth node from the end of a singly-linked list */
struct ListNode* removeNthFromEnd(struct ListNode* head, int n) {
    struct ListNode dummy = {.next = head};  /* Dummy node before head */
    struct ListNode *pDummy = &dummy;        /* Pointer to the node before 'slow' */
    struct ListNode *slow = head;            /* Will stop at the node to delete */
    struct ListNode *fast = head;            /* Moves n steps ahead of 'slow' */
    int i = 1;

    /* If there is only one node, remove it directly */
    if (!head->next) {
        free(head);
        return NULL;
    }

    /* Move 'fast' pointer n steps ahead */
    while (fast && i < n) {
        fast = fast->next;
        i++;
    }

    /* Move both pointers until 'fast' reaches the end */
    while (fast && fast->next) {
        pDummy = pDummy->next;  /* Tracks node before 'slow' */
        slow = slow->next;      /* Node to be removed */
        fast = fast->next;
    }

    /* Remove the nth node from the end */
    pDummy->next = slow->next;
    free(slow);

    /* Return the new head (dummy.next handles removing the first node case) */
    return dummy.next;
}
```
