[21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/description/)

```c
/* 21. Merge Two Sorted Lists */

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */

/* Merge two sorted linked lists into a single sorted list */
struct ListNode* mergeTwoLists(struct ListNode* list1, struct ListNode* list2) {
    struct ListNode dummy;                 /* Dummy node to simplify list handling */
    struct ListNode *pDummy = &dummy;      /* Pointer to the current end of the merged list */
    struct ListNode *newlist = pDummy;     /* Keep track of the head (dummy node) */
    struct ListNode *head1 = list1;
    struct ListNode *head2 = list2;

    /* Handle cases where one or both lists are empty */
    if (!list1 && !list2)
        return NULL;
    if (!list1)
        return list2;
    if (!list2)
        return list1;

    /* Compare nodes from both lists and attach the smaller one each time */
    while (head1 && head2) {
        if (head1->val < head2->val) {
            pDummy->next = head1;
            head1 = head1->next;
        } else {
            pDummy->next = head2;
            head2 = head2->next;
        }
        pDummy = pDummy->next;
    }

    /* Attach any remaining nodes from either list */
    if (head1)
        pDummy->next = head1;

    if (head2)
        pDummy->next = head2;

    /* Return the merged list (skipping dummy node) */
    return newlist->next;
}
```
