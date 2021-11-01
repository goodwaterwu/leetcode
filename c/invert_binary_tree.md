[Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)

![image](https://github.com/goodwaterwu/leetcode/blob/master/c/images/invert_binary_tree.png?raw=true)

```c
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 * int val;
 * struct TreeNode *left;
 * struct TreeNode *right;
 * };
 */

struct TreeNode* invertTree(struct TreeNode *root)
{
	struct TreeNode *tmp = NULL;

	if (!root)
		return NULL;

	tmp = root->left;
	root->left = root->right;
	root->right = tmp;
	invertTree(root->left);
	invertTree(root->right);

	return root;
}
```
