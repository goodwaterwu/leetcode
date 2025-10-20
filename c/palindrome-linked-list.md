[234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)

```c
/* 234. Palindrome Linked List */

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
bool isPalindrome(struct ListNode* head) {
    struct ListNode *slow = head;  /* Slow pointer moves 1 step */
    struct ListNode *fast = head;  /* Fast pointer moves 2 steps */

    /* Find the middle of the list */
    while (fast->next && fast->next->next) {
        slow = slow->next;
        fast = fast->next->next;
    }

    /* Reverse the second half of the list starting from slow */
    struct ListNode *prev = NULL;
    struct ListNode *current = slow;
    while (current) {
        struct ListNode *tmp = current->next;
        current->next = prev;
        prev = current;
        current = tmp;
    }

    /* Compare the first half and the reversed second half */
    while (head && prev) {
        if (head->val != prev->val)
            return false;
        head = head->next;
        prev = prev->next;
    }

    return true;
}
```
