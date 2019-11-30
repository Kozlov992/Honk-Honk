# Trees

+ [Binary Tree Inorder Traversal](#binary-tree-inorder-traversal)
+ [Symmetric Tree](#symmetric-tree)
+ [Maximum Depth of Binary Tree](#maximum-depth-of-binary-tree)
+ [Same Tree](#same-tree)
+ [Invert Binary Tree](#invert-binary-tree)
+ [Path Sum](#path-sum)
+ [Subtree of Another Tree](#subtree-of-another-tree)
+ [Binary Tree Level Order Traversal](#binary-tree-level-order-traversal)
+ [Kth Smallest Element in a BST](#kth-smallest-element-in-a-bst)
+ [Validate Binary Search Tree](#validate-binary-search-tree)
+ [Binary Search Tree Iterator](#binary-search-tree-iterator)
+ [Inorder Successor in BST](#inorder-successor-in-bst)
+ [Lowest Common Ancestor of a Binary Search Tree](#lowest-common-ancestor-of-a-binary-search-tree)
+ [Lowest Common Ancestor of a Binary Tree](#lowest-common-ancestor-of-a-binary-tree)

## Binary Tree Inorder Traversal

https://leetcode.com/problems/binary-tree-inorder-traversal/

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    void FindOrder(TreeNode* root, vector<int>& InOrder) {
        if (root == NULL)
            return;
        if (root->left != NULL)
            FindOrder(root->left, InOrder);
        InOrder.push_back(root->val);
        if (root->right != NULL)
            FindOrder(root->right, InOrder);
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> InOrder(0);
        FindOrder(root, InOrder);
        return InOrder;
    }
};
```

## Symmetric Tree

https://leetcode.com/problems/symmetric-tree/

```C++
class Solution {
public:
    bool isMirror(TreeNode* left, TreeNode* right) {
        if (left == NULL && right == NULL)
            return true;
        if (left == NULL || right == NULL)
            return false;
        return left->val == right->val && isMirror(left->left, right->right) && isMirror(left->right, right->left);
    }
    bool isSymmetric(TreeNode* root) {
        if (root == NULL)
            return true;
        return isMirror(root->left, root->right);
    }
};
```

## Maximum Depth of Binary Tree

https://leetcode.com/problems/maximum-depth-of-binary-tree/

```C++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        return (root == NULL) ? 0 : (max(maxDepth(root->left), maxDepth(root->right)) + 1);
    }
};
```

## Same Tree

https://leetcode.com/problems/same-tree/

```C++
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (p == NULL && q == NULL)
            return true;
        if (p == NULL || q == NULL)
            return false;
        return p->val == q->val && isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
    }
};
```

## Invert Binary Tree

https://leetcode.com/problems/invert-binary-tree/

```C++
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (root == NULL)
            return NULL;
        TreeNode* right = invertTree(root->right);
        TreeNode* left = invertTree(root->left);
        root->left = right;
        root->right = left;
        return root;
    }
};
```

## Path Sum

https://leetcode.com/problems/path-sum/

```C++
class Solution {
public:
    bool hasPathSum(TreeNode* root, int sum) {
        if (root == NULL)
            return false;
        if (root->val == sum && root->left == NULL && root->right == NULL)
            return true;
        return (hasPathSum(root->left, sum - root->val) || hasPathSum(root->right, sum - root->val));
    }
};
```

## Subtree of Another Tree

https://leetcode.com/problems/subtree-of-another-tree/submissions/

```C++
class Solution {
private:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (p == NULL && q == NULL)
            return true;
        if (p == NULL || q == NULL)
            return false;
        return p->val == q->val && isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
    }
public:
    bool isSubtree(TreeNode* s, TreeNode* t) {
        if (s == NULL && t == NULL)
            return true;
        if (s == NULL || t == NULL)
            return false;
        return isSameTree(s,t) || isSubtree(s->left, t) || isSubtree(s->right, t); 
    }
};
```

## Binary Tree Level Order Traversal

https://leetcode.com/problems/binary-tree-level-order-traversal/

```C++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        levelOrder(root, result, 0);
        return result;
    }
    void levelOrder(TreeNode* root, vector<vector<int>>& result, int level) {
        if (!root)
            return;
        if (level == result.size())
    	    result.push_back(vector<int> {});
        result[level].push_back(root->val);
        levelOrder(root->left, result, level + 1);
        levelOrder(root->right, result, level + 1);
    }
};
```

## Kth Smallest Element in a BST

https://leetcode.com/problems/kth-smallest-element-in-a-bst/

```C++
class Solution {
public:
    void FindOrder(TreeNode* root, vector<int>& InOrder) {
        if (root == NULL)
            return;
        if (root->left != NULL)
            FindOrder(root->left, InOrder);
        InOrder.push_back(root->val);
        if (root->right != NULL)
            FindOrder(root->right, InOrder);
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> InOrder(0);
        FindOrder(root, InOrder);
        return InOrder;
    }
    int kthSmallest(TreeNode* root, int k) {
        vector<int> InOrder = inorderTraversal(root);
        return InOrder[k - 1];
    }
};
```

## Validate Binary Search Tree

https://leetcode.com/problems/validate-binary-search-tree/

```C++
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        return isValidBST(root, NULL, NULL);
    }

    bool isValidBST(TreeNode* root, TreeNode* min, TreeNode* max) {
        if (!root) return true;
        if (min && root->val <= min->val || max && root->val >= max->val)
            return false;
        return isValidBST(root->left, min, root) && isValidBST(root->right, root, max);
    }
};
```

## Binary Search Tree Iterator

https://leetcode.com/problems/binary-search-tree-iterator/

```C++
class BSTIterator {
public:
    stack<TreeNode*> Stack;
    BSTIterator(TreeNode* root) {
        PushToTheLeft(root);
    }
    
    /** @return the next smallest number */
    int next() {
        TreeNode *tmp = Stack.top();
        Stack.pop();
        PushToTheLeft(tmp->right);
        return tmp->val;
    }
    
    /** @return whether we have a next smallest number */
    bool hasNext() {
        return !Stack.empty();
    }
    private:
    void PushToTheLeft(TreeNode* root) {
        while (root) {
            Stack.push(root);
            root = root->left;
        }
    }
};
```

## Inorder Successor in BST

https://www.lintcode.com/problem/inorder-successor-in-bst/

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */


class Solution {
public:
    TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
        if (!root)
            return NULL;
        if (root->val <= p->val)
            return inorderSuccessor(root->right, p);
        TreeNode* left = inorderSuccessor(root->left, p);
        return left == NULL ? root : left;
    }
};
```

## Lowest Common Ancestor of a Binary Search Tree

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/

```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        while (root &&  ((root->val - p->val) * (root->val - q->val) > 0))
            root = p->val < root->val ? root->left : root->right;
        return root;
    }
};
```

## Lowest Common Ancestor of a Binary Tree

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root || root == p || root == q) return root;
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);
        return (!left) ? (right) : ( (!right) ? (left) : (root) );
    }
};
```
