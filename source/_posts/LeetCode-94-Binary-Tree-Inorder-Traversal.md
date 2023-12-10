---
title: LeetCode 94. Binary Tree Inorder Traversal
lang: en
date: 2023-12-10 09:06:50
tags:
    - LeetCode
    - Algorithm
    - Binary tree
    - Recursion
categories:
    - LeetCode
---

## Intuition
- Traverse the left subtree.
- Visit the root node.
- Traverse the right subtree.

## Approach 1: Recursion

- Implement the traversal process recursively.

Pseudocode of this approach:

```
path[]
traverse(root):
	Input root of a binary tree
	
	if root = NULL then
		return
	end if
	traverse(left(root))
	add root to path
	traverse(right(root))
	return
```

### Complexity
Time complexity: $O(n)$.

- Every node in the binary tree will be visited once.

Space complexity: $O(n)$.

- In the worst case (all nodes in the tree only have left or right subtrees), the length of the function call stack will be $n$.

### Code
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
  void traverse(TreeNode* root, vector<int> *path) {
    if (root == nullptr) {
      return;
    }
    traverse(root->left, path);
    path->push_back(root->val);
    traverse(root->right, path);
    return;
  }

  vector<int> inorderTraversal(TreeNode* root) {
    vector<int> *path = new vector<int>();
    traverse(root, path);
    return *path;
  }
};
```

## Approach 2: Stack

- Goes to the leftmost node in the tree while pushing the nodes onto a stack.
- After reaching the leftmost node, pop a node from the stack and visit it, then move to its right subtree.
- Repeat until all nodes are visited.

Pseudocode of this approach:

```
inorderTraversal(root):
	Input root of a binary tree
	
	path[]
	st = empty stack
	while p != NULL and st is not empty do
		while p != NULL do
			push p onto st
			p = left(p)
		end while
		pop p from st
		add p to path
		p = right(p)
	end while
```

### Complexity

Time complexity: $O(n)$.

- $n$ loops in total to visit every node once.

Space complexity: $O(n)$.

- In the worst case, the length of the stack will be $n$.

### Code

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
  vector<int> inorderTraversal(TreeNode* root) {
    vector<int> path;
    stack<TreeNode *> st;
    TreeNode *p = root;
    while (p != nullptr || !st.empty()) {
      while (p != nullptr) {
        // Find the leftmost node in the tree
        st.push(p);
        p = p->left;
      }
      // Traverse the right subtree
      p = st.top();
      st.pop();
      path.push_back(p->val);
      p = p->right;
    }
    return path;
  }
};
```

## Approach 3: Morris Traversal

Reference: [Wikipedia](https://en.wikipedia.org/wiki/Tree_traversal#Morris_in-order_traversal_using_threading)

Pseudocode of this approach:

```
inorderTraversal(root):
	Input root of a binary tree
	
	path[]
	p = root
	while p != NULL do
		if left(p) == null then
			add p to path
			// Move to its right subtree
			p = right(p)
		else
			// pre is the predecessor of p
			pre = left(p)
			// Find the rightmost node in the right subtree
			while right(p) != NULL do
				pre = right(pre)
			end while
			// Put p after pre
			right(pre) = p
			// Unlink the original left subtree from the binary tree
			parent = p
			p = left(p)
			left(parent) = NULL
		end if
	end while
```

### Complexity

Time complexity: $O(n)$.

- $n$ loops in total to traverse the binary tree.

Space complexity: $O(1)$.

### Code

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
  vector<int> inorderTraversal(TreeNode* root) {
    vector<int> path;
    TreeNode *p = root;
    while (p != nullptr) {
      if (p->left == nullptr) {
        path.push_back(p->val);
        p = p->right;
      } else {
        TreeNode *pre = p->left;
        while (pre->right != nullptr) {
          pre = pre->right;
        }
        pre->right = p;
        TreeNode *parent = p;
        p = p->left;
        parent->left = nullptr;
      }
    }
    return path;
  }
};
```
