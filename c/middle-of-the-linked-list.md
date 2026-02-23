[876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/description/)

```c
/* 876. Middle of the Linked List - Two Pointers (Fast and Slow Pointer Technique) */

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* middleNode(struct ListNode* head) {
    /* Slow pointer moves one step at a time */
    struct ListNode *i = head;
    /* Fast pointer moves two steps at a time */
    struct ListNode *j = head;

    /* When fast pointer reaches the end, slow pointer will be at the middle */
    while (j && j->next) {
        i = i->next;
        j = j->next->next;
    }

    /* Return the middle node */
    return i;
}
```
