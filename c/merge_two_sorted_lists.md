[Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *	 int val;
 *	 struct ListNode *next;
 * };
 */

#define LIST_MAX 100

struct ListNode nodes[LIST_MAX];

struct ListNode *mergeTwoLists(struct ListNode *l1, struct ListNode *l2)
{
	struct ListNode *list1 = l1;
	struct ListNode *list2 = l2;
	size_t l1_size = 0;
	size_t l2_size = 0;
	size_t new_size = 0;

	/* Reset list. */
	memset(&nodes, 0, sizeof(struct ListNode) * LIST_MAX);

	/* Count l1 size. */
	while (list1) {
		l1_size++;
		list1 = list1->next;
	}

	/* Count l2 size. */
	while (list2) {
		l2_size++;
		list2 = list2->next;
	}

	/* Count new list size. */
	new_size = l1_size + l2_size;
	if (!new_size)
		return NULL;

	for (size_t i = 0; i != new_size; i++) {
		if (l1 && l2) {
			if (l1->val < l2->val) {
				nodes[i].val = l1->val;
				l1 = l1->next;
			} else {
				nodes[i].val = l2->val;
				l2 = l2->next;
			}
		} else if (l1) {
			nodes[i].val = l1->val;
			l1 = l1->next;
		} else {
			nodes[i].val = l2->val;
			l2 = l2->next;
		}

		if (i != new_size - 1 && i + 1 < LIST_MAX)
			nodes[i].next = nodes + i + 1;
	}

	return &nodes;
}
```
