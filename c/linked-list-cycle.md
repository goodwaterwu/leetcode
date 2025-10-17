[141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/description/)

```c
/* 141. Linked List Cycle */

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */

/* Detect if a linked list has a cycle using Floyd’s Tortoise and Hare algorithm */
bool hasCycle(struct ListNode *head) {
    struct ListNode *slow = head;   /* Slow pointer (moves 1 step at a time) */
    struct ListNode *fast = head;  /* Fast pointer (moves 2 steps at a time) */

    /* Traverse the list */
    while (fast && fast->next) {
        slow = slow->next;           /* Move slow pointer by one */
        fast = fast->next->next;   /* Move fast pointer by two */

        /* If the two pointers meet, a cycle exists */
        if (slow == fast)
            return true;
    }

    /* If fast reaches the end, there is no cycle */
    return false;
}
```
