[23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/description/)

```c
/* 23. Merge k Sorted Lists */
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */

/*
 * Merge two sorted linked lists into a single sorted linked list.
 * list1 and list2 are assumed to be sorted in ascending order.
 * The function reuses existing nodes and returns the head of the merged list.
 */
struct ListNode *merge_two_lists(struct ListNode *list1, struct ListNode *list2) {
    /* If both lists are empty, return NULL */
    if (!list1 && !list2)
        return NULL;

    /* Create a dummy head node to simplify list construction */
    struct ListNode *new_list = (struct ListNode *)malloc(sizeof(struct ListNode));
    struct ListNode *p = new_list;
    struct ListNode *tmp = NULL;

    /* Merge nodes from both lists while neither is empty */
    while (list1 && list2) {
        /* Attach the node with the smaller value */
        if (list1->val <= list2->val) {
            p->next = list1;
            list1 = list1->next;
        } else {
            p->next = list2;
            list2 = list2->next;
        }

        /* Move the pointer forward in the merged list */
        p = p->next;
    }

    /* If there are remaining nodes in list1, append them */
    if (list1) {
        p->next = list1;
        p = p->next;
    }

    /* If there are remaining nodes in list2, append them */
    if (list2) {
        p->next = list2;
        p = p->next;
    }

    /* Remove the dummy head and return the real head */
    tmp = new_list;
    new_list = new_list->next;
    free(tmp);

    return new_list;
}

/*
 * Merge k sorted linked lists into one sorted linked list.
 * The lists are merged in pairs repeatedly until only one list remains.
 */
struct ListNode* mergeKLists(struct ListNode** lists, int listsSize) {
    /* If there are no lists, return NULL */
    if (listsSize == 0)
        return NULL;

    /* Continue merging until only one list remains */
    while (1) {
        int index = 0;

        /* Merge lists in pairs: lists[i] with lists[i + 1] */
        for (int i = 0; i < listsSize; i += 2) {
            if (i + 1 < listsSize)
                lists[index] = merge_two_lists(lists[i], lists[i + 1]);
            else
                /* If there is an odd list out, carry it forward */
                lists[index] = lists[i];

            index++;
        }

        /* If only one merged list remains, stop */
        if (index == 1)
            break;

        /* Update the number of lists for the next iteration */
        listsSize = index;
    }

    /* Return the final merged sorted list */
    return lists[0];
}
```
