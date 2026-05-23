# Binary Tree Easy LeetCode — C++ Notes & Solutions

> **TreeNode definition (assumed throughout):**
> ```cpp
> struct TreeNode {
>     int val;
>     TreeNode *left, *right;
>     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
> };
> ```

---

## 📋 Problem Index

| # | Problem | Link |
|---|---------|------|
| 94 | [Binary Tree Inorder Traversal](#94-binary-tree-inorder-traversal) | [LeetCode](https://leetcode.com/problems/binary-tree-inorder-traversal) |
| 100 | [Same Tree](#100-same-tree) | [LeetCode](https://leetcode.com/problems/same-tree) |
| 101 | [Symmetric Tree](#101-symmetric-tree) | [LeetCode](https://leetcode.com/problems/symmetric-tree) |
| 104 | [Maximum Depth of Binary Tree](#104-maximum-depth-of-binary-tree) | [LeetCode](https://leetcode.com/problems/maximum-depth-of-binary-tree) |
| 108 | [Convert Sorted Array to BST](#108-convert-sorted-array-to-binary-search-tree) | [LeetCode](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree) |
| 110 | [Balanced Binary Tree](#110-balanced-binary-tree) | [LeetCode](https://leetcode.com/problems/balanced-binary-tree) |
| 111 | [Minimum Depth of Binary Tree](#111-minimum-depth-of-binary-tree) | [LeetCode](https://leetcode.com/problems/minimum-depth-of-binary-tree) |
| 112 | [Path Sum](#112-path-sum) | [LeetCode](https://leetcode.com/problems/path-sum) |
| 144 | [Binary Tree Preorder Traversal](#144-binary-tree-preorder-traversal) | [LeetCode](https://leetcode.com/problems/binary-tree-preorder-traversal) |
| 145 | [Binary Tree Postorder Traversal](#145-binary-tree-postorder-traversal) | [LeetCode](https://leetcode.com/problems/binary-tree-postorder-traversal) |
| 222 | [Count Complete Tree Nodes](#222-count-complete-tree-nodes) | [LeetCode](https://leetcode.com/problems/count-complete-tree-nodes) |
| 226 | [Invert Binary Tree](#226-invert-binary-tree) | [LeetCode](https://leetcode.com/problems/invert-binary-tree) |
| 257 | [Binary Tree Paths](#257-binary-tree-paths) | [LeetCode](https://leetcode.com/problems/binary-tree-paths) |
| 270 | [Closest BST Value](#270-closest-binary-search-tree-value) | [LeetCode](https://leetcode.com/problems/closest-binary-search-tree-value) |
| 404 | [Sum of Left Leaves](#404-sum-of-left-leaves) | [LeetCode](https://leetcode.com/problems/sum-of-left-leaves) |
| 501 | [Find Mode in BST](#501-find-mode-in-binary-search-tree) | [LeetCode](https://leetcode.com/problems/find-mode-in-binary-search-tree) |
| 530 | [Minimum Absolute Difference in BST](#530-minimum-absolute-difference-in-bst) | [LeetCode](https://leetcode.com/problems/minimum-absolute-difference-in-bst) |
| 543 | [Diameter of Binary Tree](#543-diameter-of-binary-tree) | [LeetCode](https://leetcode.com/problems/diameter-of-binary-tree) |
| 559 | [Maximum Depth of N-ary Tree](#559-maximum-depth-of-n-ary-tree) | [LeetCode](https://leetcode.com/problems/maximum-depth-of-n-ary-tree) |
| 563 | [Binary Tree Tilt](#563-binary-tree-tilt) | [LeetCode](https://leetcode.com/problems/binary-tree-tilt) |
| 572 | [Subtree of Another Tree](#572-subtree-of-another-tree) | [LeetCode](https://leetcode.com/problems/subtree-of-another-tree) |
| 589 | [N-ary Tree Preorder Traversal](#589-n-ary-tree-preorder-traversal) | [LeetCode](https://leetcode.com/problems/n-ary-tree-preorder-traversal) |
| 590 | [N-ary Tree Postorder Traversal](#590-n-ary-tree-postorder-traversal) | [LeetCode](https://leetcode.com/problems/n-ary-tree-postorder-traversal) |
| 617 | [Merge Two Binary Trees](#617-merge-two-binary-trees) | [LeetCode](https://leetcode.com/problems/merge-two-binary-trees) |
| 637 | [Average of Levels in Binary Tree](#637-average-of-levels-in-binary-tree) | [LeetCode](https://leetcode.com/problems/average-of-levels-in-binary-tree) |
| 653 | [Two Sum IV - Input is a BST](#653-two-sum-iv---input-is-a-bst) | [LeetCode](https://leetcode.com/problems/two-sum-iv-input-is-a-bst) |
| 671 | [Second Minimum Node in Binary Tree](#671-second-minimum-node-in-a-binary-tree) | [LeetCode](https://leetcode.com/problems/second-minimum-node-in-a-binary-tree) |
| 700 | [Search in a BST](#700-search-in-a-binary-search-tree) | [LeetCode](https://leetcode.com/problems/search-in-a-binary-search-tree) |
| 703 | [Kth Largest Element in a Stream](#703-kth-largest-element-in-a-stream) | [LeetCode](https://leetcode.com/problems/kth-largest-element-in-a-stream) |
| 783 | [Minimum Distance Between BST Nodes](#783-minimum-distance-between-bst-nodes) | [LeetCode](https://leetcode.com/problems/minimum-distance-between-bst-nodes) |
| 872 | [Leaf-Similar Trees](#872-leaf-similar-trees) | [LeetCode](https://leetcode.com/problems/leaf-similar-trees) |
| 897 | [Increasing Order Search Tree](#897-increasing-order-search-tree) | [LeetCode](https://leetcode.com/problems/increasing-order-search-tree) |
| 938 | [Range Sum of BST](#938-range-sum-of-bst) | [LeetCode](https://leetcode.com/problems/range-sum-of-bst) |
| 965 | [Univalued Binary Tree](#965-univalued-binary-tree) | [LeetCode](https://leetcode.com/problems/univalued-binary-tree) |
| 993 | [Cousins in Binary Tree](#993-cousins-in-binary-tree) | [LeetCode](https://leetcode.com/problems/cousins-in-binary-tree) |
| 1022 | [Sum of Root To Leaf Binary Numbers](#1022-sum-of-root-to-leaf-binary-numbers) | [LeetCode](https://leetcode.com/problems/sum-of-root-to-leaf-binary-numbers) |
| 1379 | [Find Corresponding Node in Clone](#1379-find-a-corresponding-node-of-a-binary-tree-in-a-clone-of-that-tree) | [LeetCode](https://leetcode.com/problems/find-a-corresponding-node-of-a-binary-tree-in-a-clone-of-that-tree) |
| 1469 | [Find All The Lonely Nodes](#1469-find-all-the-lonely-nodes) | [LeetCode](https://leetcode.com/problems/find-all-the-lonely-nodes) |
| 2236 | [Root Equals Sum of Children](#2236-root-equals-sum-of-children) | [LeetCode](https://leetcode.com/problems/root-equals-sum-of-children) |
| 2331 | [Evaluate Boolean Binary Tree](#2331-evaluate-boolean-binary-tree) | [LeetCode](https://leetcode.com/problems/evaluate-boolean-binary-tree) |
| 2689 | [Extract Kth Character From Rope Tree](#2689-extract-kth-character-from-the-rope-tree) | [LeetCode](https://leetcode.com/problems/extract-kth-character-from-the-rope-tree) |

---

## 94. Binary Tree Inorder Traversal
🔗 [LeetCode](https://leetcode.com/problems/binary-tree-inorder-traversal)

**Logic:** Inorder = Left → Root → Right. The recursion naturally captures this order: go as deep left as possible first, record the node, then process the right. The result comes out sorted for a BST.

```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;
        dfs(root, result);
        return result;
    }

    void dfs(TreeNode* node, vector<int>& result) {
        if (!node) return;
        dfs(node->left, result);        // visit entire left subtree first
        result.push_back(node->val);    // record current node (root)
        dfs(node->right, result);       // visit entire right subtree last
    }
};
```

---

## 100. Same Tree
🔗 [LeetCode](https://leetcode.com/problems/same-tree)

**Logic:** Two trees are the same if: both are null (trivially same), OR both are non-null with equal values AND their left subtrees match AND their right subtrees match. Any mismatch anywhere returns false.

```cpp
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (!p && !q) return true;          // both null → same
        if (!p || !q) return false;         // one null, one not → different
        if (p->val != q->val) return false; // values differ → different
        // both must match recursively
        return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
    }
};
```

---

## 101. Symmetric Tree
🔗 [LeetCode](https://leetcode.com/problems/symmetric-tree)

**Logic:** A tree is symmetric if its left subtree is a mirror image of its right. Write a helper `isMirror(l, r)`: values must match, the outer pair (l->left, r->right) must mirror, and the inner pair (l->right, r->left) must mirror.

```cpp
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        return isMirror(root->left, root->right);
    }

    bool isMirror(TreeNode* l, TreeNode* r) {
        if (!l && !r) return true;
        if (!l || !r) return false;
        return (l->val == r->val) &&
               isMirror(l->left, r->right) &&   // outer pair must mirror
               isMirror(l->right, r->left);      // inner pair must mirror
    }
};
```

---

## 104. Maximum Depth of Binary Tree
🔗 [LeetCode](https://leetcode.com/problems/maximum-depth-of-binary-tree)

**Logic:** The depth of any node = 1 + max(depth of left child, depth of right child). Base case: a null node has depth 0. The recursion naturally bubbles the maximum depth up to the root.

```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (!root) return 0;
        int leftDepth  = maxDepth(root->left);
        int rightDepth = maxDepth(root->right);
        return 1 + max(leftDepth, rightDepth);  // current node adds 1 level
    }
};
```

---

## 108. Convert Sorted Array to Binary Search Tree
🔗 [LeetCode](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree)

**Logic:** To get a height-balanced BST from a sorted array, always pick the middle element as the root — this ensures equal (or off-by-one) number of elements on both sides. Recurse on the left half for the left subtree and right half for the right subtree.

```cpp
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return build(nums, 0, nums.size() - 1);
    }

    TreeNode* build(vector<int>& nums, int lo, int hi) {
        if (lo > hi) return nullptr;
        int mid = lo + (hi - lo) / 2;              // middle element becomes root
        TreeNode* node = new TreeNode(nums[mid]);
        node->left  = build(nums, lo, mid - 1);    // left half → left subtree
        node->right = build(nums, mid + 1, hi);    // right half → right subtree
        return node;
    }
};
```

---

## 110. Balanced Binary Tree
🔗 [LeetCode](https://leetcode.com/problems/balanced-binary-tree)

**Logic:** A tree is balanced if for every node |height(left) - height(right)| ≤ 1. Use a helper that returns the actual height OR -1 as a sentinel meaning "already unbalanced." Once -1 is detected anywhere, it propagates all the way up, short-circuiting further checks.

```cpp
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        return height(root) != -1;
    }

    int height(TreeNode* node) {
        if (!node) return 0;
        int lh = height(node->left);
        if (lh == -1) return -1;                  // left subtree is unbalanced
        int rh = height(node->right);
        if (rh == -1) return -1;                  // right subtree is unbalanced
        if (abs(lh - rh) > 1) return -1;          // current node is unbalanced
        return 1 + max(lh, rh);                   // return actual height
    }
};
```

---

## 111. Minimum Depth of Binary Tree
🔗 [LeetCode](https://leetcode.com/problems/minimum-depth-of-binary-tree)

**Logic:** Min depth = shortest root-to-leaf path. Key pitfall: if a node has only one child, the empty-child side is NOT a leaf — we must recurse only into the existing child. Only when both children exist do we take the minimum.

```cpp
class Solution {
public:
    int minDepth(TreeNode* root) {
        if (!root) return 0;
        if (!root->left)  return 1 + minDepth(root->right); // only right child exists
        if (!root->right) return 1 + minDepth(root->left);  // only left child exists
        return 1 + min(minDepth(root->left), minDepth(root->right));
    }
};
```

---

## 112. Path Sum
🔗 [LeetCode](https://leetcode.com/problems/path-sum)

**Logic:** Subtract the current node's value from the target at each step. If we reach a leaf and the remaining target is exactly 0, we found a valid path. We must check the leaf condition before recursing, otherwise internal nodes with two children could falsely match.

```cpp
class Solution {
public:
    bool hasPathSum(TreeNode* root, int targetSum) {
        if (!root) return false;
        targetSum -= root->val;                          // consume current node's value
        if (!root->left && !root->right)                 // reached a leaf
            return targetSum == 0;
        return hasPathSum(root->left, targetSum) ||
               hasPathSum(root->right, targetSum);
    }
};
```

---

## 144. Binary Tree Preorder Traversal
🔗 [LeetCode](https://leetcode.com/problems/binary-tree-preorder-traversal)

**Logic:** Preorder = Root → Left → Right. Record the current node first before descending into any children.

```cpp
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        dfs(root, result);
        return result;
    }

    void dfs(TreeNode* node, vector<int>& result) {
        if (!node) return;
        result.push_back(node->val);   // record root FIRST
        dfs(node->left, result);
        dfs(node->right, result);
    }
};
```

---

## 145. Binary Tree Postorder Traversal
🔗 [LeetCode](https://leetcode.com/problems/binary-tree-postorder-traversal)

**Logic:** Postorder = Left → Right → Root. Process both children completely before recording the current node.

```cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> result;
        dfs(root, result);
        return result;
    }

    void dfs(TreeNode* node, vector<int>& result) {
        if (!node) return;
        dfs(node->left, result);
        dfs(node->right, result);
        result.push_back(node->val);   // record root LAST
    }
};
```

---

## 222. Count Complete Tree Nodes
🔗 [LeetCode](https://leetcode.com/problems/count-complete-tree-nodes)

**Logic:** Naive O(n) works but we can do O(log²n). Measure leftmost depth and rightmost depth. If equal, the tree is a perfect binary tree → node count = 2^h - 1 (use bit shift). If unequal, recurse on both subtrees — but one of them will always be perfect and resolve in O(1).

```cpp
class Solution {
public:
    int countNodes(TreeNode* root) {
        if (!root) return 0;
        int lh = 0, rh = 0;
        TreeNode *l = root, *r = root;
        while (l) { lh++; l = l->left; }   // leftmost depth
        while (r) { rh++; r = r->right; }  // rightmost depth
        if (lh == rh)
            return (1 << lh) - 1;           // perfect tree: 2^h - 1
        return 1 + countNodes(root->left) + countNodes(root->right);
    }
};
```

---

## 226. Invert Binary Tree
🔗 [LeetCode](https://leetcode.com/problems/invert-binary-tree)

**Logic:** Swap left and right children at every node. Do it top-down: swap first, then recurse into the (already-swapped) children. The tree mirrors itself recursively.

```cpp
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (!root) return nullptr;
        swap(root->left, root->right);      // swap children at current node
        invertTree(root->left);
        invertTree(root->right);
        return root;
    }
};
```

---

## 257. Binary Tree Paths
🔗 [LeetCode](https://leetcode.com/problems/binary-tree-paths)

**Logic:** DFS while carrying the current path string. At each node, append its value. At a leaf, save the complete path. Pass path by value (not reference) so that backtracking is handled automatically — each recursive call gets its own copy.

```cpp
class Solution {
public:
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> result;
        dfs(root, "", result);
        return result;
    }

    void dfs(TreeNode* node, string path, vector<string>& result) {
        if (!node) return;
        path += to_string(node->val);
        if (!node->left && !node->right) {   // leaf: save completed path
            result.push_back(path);
            return;
        }
        dfs(node->left,  path + "->", result);
        dfs(node->right, path + "->", result);
    }
};
```

---

## 270. Closest Binary Search Tree Value
🔗 [LeetCode](https://leetcode.com/problems/closest-binary-search-tree-value)

**Logic:** Exploit BST property for O(h) search. At each node, update the closest value seen so far. Since BST is ordered, if target < node->val, the answer can only get closer going left; if target > node->val, go right. No need to check both sides.

```cpp
class Solution {
public:
    int closestValue(TreeNode* root, double target) {
        int closest = root->val;
        while (root) {
            // update closest if current node is nearer to target
            if (abs(root->val - target) < abs(closest - target))
                closest = root->val;
            root = target < root->val ? root->left : root->right;
        }
        return closest;
    }
};
```

---

## 404. Sum of Left Leaves
🔗 [LeetCode](https://leetcode.com/problems/sum-of-left-leaves)

**Logic:** We need to distinguish left leaves from right leaves, so we pass a boolean `isLeft` flag down. At each leaf, add its value only if `isLeft` is true. Non-leaf nodes contribute nothing directly — they just pass the flag correctly to their children.

```cpp
class Solution {
public:
    int sumOfLeftLeaves(TreeNode* root) {
        return dfs(root, false);
    }

    int dfs(TreeNode* node, bool isLeft) {
        if (!node) return 0;
        if (!node->left && !node->right)         // leaf node
            return isLeft ? node->val : 0;
        return dfs(node->left, true) + dfs(node->right, false);
    }
};
```

---

## 501. Find Mode in Binary Search Tree
🔗 [LeetCode](https://leetcode.com/problems/find-mode-in-binary-search-tree)

**Logic:** Inorder traversal of a BST yields values in sorted order, so equal values are always consecutive. Track: the previous value, the current run length, and the maximum run length seen. Whenever the run equals the max, add to result; when it exceeds the max, clear result and start fresh.

```cpp
class Solution {
    int prev = INT_MIN, count = 0, maxCount = 0;
    vector<int> result;
public:
    vector<int> findMode(TreeNode* root) {
        inorder(root);
        return result;
    }

    void inorder(TreeNode* node) {
        if (!node) return;
        inorder(node->left);

        count = (node->val == prev) ? count + 1 : 1;  // extend or reset streak
        prev = node->val;

        if (count > maxCount) {
            maxCount = count;
            result = {node->val};       // new mode found, reset result
        } else if (count == maxCount) {
            result.push_back(node->val);
        }

        inorder(node->right);
    }
};
```

---

## 530. Minimum Absolute Difference in BST
🔗 [LeetCode](https://leetcode.com/problems/minimum-absolute-difference-in-bst)

**Logic:** Inorder traversal gives sorted values. The minimum absolute difference always occurs between two adjacent values in sorted order — so we only need to compare each node with the immediately previous node in the inorder sequence.

```cpp
class Solution {
    int prev = -1, minDiff = INT_MAX;
public:
    int getMinimumDifference(TreeNode* root) {
        inorder(root);
        return minDiff;
    }

    void inorder(TreeNode* node) {
        if (!node) return;
        inorder(node->left);
        if (prev != -1)
            minDiff = min(minDiff, node->val - prev); // diff with previous node
        prev = node->val;
        inorder(node->right);
    }
};
```

---

## 543. Diameter of Binary Tree
🔗 [LeetCode](https://leetcode.com/problems/diameter-of-binary-tree)

**Logic:** The diameter through any node = leftHeight + rightHeight (number of edges). The global answer might pass through any node, not just the root, so we track a global max. The recursion returns heights upward while updating the diameter at each node as a side effect.

```cpp
class Solution {
    int maxDiameter = 0;
public:
    int diameterOfBinaryTree(TreeNode* root) {
        height(root);
        return maxDiameter;
    }

    int height(TreeNode* node) {
        if (!node) return 0;
        int lh = height(node->left);
        int rh = height(node->right);
        maxDiameter = max(maxDiameter, lh + rh);  // diameter through this node
        return 1 + max(lh, rh);                   // return height upward
    }
};
```

---

## 559. Maximum Depth of N-ary Tree
🔗 [LeetCode](https://leetcode.com/problems/maximum-depth-of-n-ary-tree)

**Logic:** Same idea as #104 but generalized for N children. Depth = 1 + max depth among all children. If no children exist, depth is 1 (just the root itself).

```cpp
class Solution {
public:
    int maxDepth(Node* root) {
        if (!root) return 0;
        int maxChild = 0;
        for (Node* child : root->children)
            maxChild = max(maxChild, maxDepth(child));  // find deepest child
        return 1 + maxChild;
    }
};
```

---

## 563. Binary Tree Tilt
🔗 [LeetCode](https://leetcode.com/problems/binary-tree-tilt)

**Logic:** Tilt of a node = |sum(left subtree) - sum(right subtree)|. We need subtree sums to compute tilt anyway, so the helper returns the subtree sum while accumulating tilt in a running total as a side effect. Classic "return one thing, update another" pattern.

```cpp
class Solution {
    int totalTilt = 0;
public:
    int findTilt(TreeNode* root) {
        subtreeSum(root);
        return totalTilt;
    }

    int subtreeSum(TreeNode* node) {
        if (!node) return 0;
        int l = subtreeSum(node->left);
        int r = subtreeSum(node->right);
        totalTilt += abs(l - r);         // add this node's tilt to global total
        return node->val + l + r;        // return full subtree sum
    }
};
```

---

## 572. Subtree of Another Tree
🔗 [LeetCode](https://leetcode.com/problems/subtree-of-another-tree)

**Logic:** For every node in the main tree, check if the subtree rooted there is identical to `subRoot` using an isSameTree check. If any node matches, return true. This is O(m*n) but straightforward and accepted.

```cpp
class Solution {
public:
    bool isSubtree(TreeNode* root, TreeNode* subRoot) {
        if (!root) return false;
        if (isSame(root, subRoot)) return true;          // match at current node
        return isSubtree(root->left, subRoot) ||
               isSubtree(root->right, subRoot);
    }

    bool isSame(TreeNode* s, TreeNode* t) {
        if (!s && !t) return true;
        if (!s || !t) return false;
        return s->val == t->val &&
               isSame(s->left, t->left) &&
               isSame(s->right, t->right);
    }
};
```

---

## 589. N-ary Tree Preorder Traversal
🔗 [LeetCode](https://leetcode.com/problems/n-ary-tree-preorder-traversal)

**Logic:** Preorder for N-ary: record current node first, then recurse on each child in left-to-right order.

```cpp
class Solution {
public:
    vector<int> preorder(Node* root) {
        vector<int> result;
        dfs(root, result);
        return result;
    }

    void dfs(Node* node, vector<int>& result) {
        if (!node) return;
        result.push_back(node->val);              // record node FIRST
        for (Node* child : node->children)
            dfs(child, result);
    }
};
```

---

## 590. N-ary Tree Postorder Traversal
🔗 [LeetCode](https://leetcode.com/problems/n-ary-tree-postorder-traversal)

**Logic:** Postorder for N-ary: recurse all children first in order, then record the current node.

```cpp
class Solution {
public:
    vector<int> postorder(Node* root) {
        vector<int> result;
        dfs(root, result);
        return result;
    }

    void dfs(Node* node, vector<int>& result) {
        if (!node) return;
        for (Node* child : node->children)
            dfs(child, result);
        result.push_back(node->val);              // record node LAST
    }
};
```

---

## 617. Merge Two Binary Trees
🔗 [LeetCode](https://leetcode.com/problems/merge-two-binary-trees)

**Logic:** Walk both trees simultaneously. If one node is null, simply return the other (nothing to merge, just use the existing subtree as-is). If both exist, sum their values and recurse on both pairs of children. We modify tree1 in place.

```cpp
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        if (!root1) return root2;   // root1 absent → use root2's subtree
        if (!root2) return root1;   // root2 absent → use root1's subtree
        root1->val += root2->val;   // merge: sum the values
        root1->left  = mergeTrees(root1->left,  root2->left);
        root1->right = mergeTrees(root1->right, root2->right);
        return root1;
    }
};
```

---

## 637. Average of Levels in Binary Tree
🔗 [LeetCode](https://leetcode.com/problems/average-of-levels-in-binary-tree)

**Logic:** BFS level-order traversal. Use a queue. Before processing each level, snapshot how many nodes are in the queue (that's exactly the level's size). Sum all values in that batch, divide by count, push to result.

```cpp
class Solution {
public:
    vector<double> averageOfLevels(TreeNode* root) {
        vector<double> result;
        queue<TreeNode*> q;
        q.push(root);
        while (!q.empty()) {
            int levelSize = q.size();       // number of nodes at this level
            double levelSum = 0;
            for (int i = 0; i < levelSize; i++) {
                TreeNode* node = q.front(); q.pop();
                levelSum += node->val;
                if (node->left)  q.push(node->left);
                if (node->right) q.push(node->right);
            }
            result.push_back(levelSum / levelSize);
        }
        return result;
    }
};
```

---

## 653. Two Sum IV - Input is a BST
🔗 [LeetCode](https://leetcode.com/problems/two-sum-iv-input-is-a-bst)

**Logic:** Traverse the tree and maintain a hash set of values seen so far. For each node, check if its complement (k - node->val) is already in the set. If yes, a valid pair exists. Insert the current value and continue.

```cpp
class Solution {
    unordered_set<int> seen;
public:
    bool findTarget(TreeNode* root, int k) {
        if (!root) return false;
        if (seen.count(k - root->val)) return true;  // complement already seen
        seen.insert(root->val);
        return findTarget(root->left, k) || findTarget(root->right, k);
    }
};
```

---

## 671. Second Minimum Node In a Binary Tree
🔗 [LeetCode](https://leetcode.com/problems/second-minimum-node-in-a-binary-tree)

**Logic:** In this special tree, root->val is always the global minimum. We need the smallest value strictly greater than root->val. DFS and track this candidate. Optimization: if current node's value is already >= our best candidate, no need to go deeper in that subtree.

```cpp
class Solution {
    long second = LONG_MAX;
public:
    int findSecondMinimumValue(TreeNode* root) {
        dfs(root, root->val);
        return second == LONG_MAX ? -1 : (int)second;
    }

    void dfs(TreeNode* node, int minVal) {
        if (!node) return;
        if (node->val > minVal && node->val < second)
            second = node->val;                 // found a better second minimum
        if (node->val == minVal) {              // equal to min: go deeper, answer may be further down
            dfs(node->left, minVal);
            dfs(node->right, minVal);
        }
        // if node->val > minVal: already >= second, no need to explore further
    }
};
```

---

## 700. Search in a Binary Search Tree
🔗 [LeetCode](https://leetcode.com/problems/search-in-a-binary-search-tree)

**Logic:** Classic BST search. At each node: if value matches, return it. If target is smaller, the answer must be in the left subtree. If larger, must be in the right subtree. O(h) time.

```cpp
class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
        if (!root) return nullptr;
        if (root->val == val) return root;           // found it
        if (val < root->val) return searchBST(root->left, val);   // go left
        return searchBST(root->right, val);          // go right
    }
};
```

---

## 703. Kth Largest Element in a Stream
🔗 [LeetCode](https://leetcode.com/problems/kth-largest-element-in-a-stream)

**Logic:** Maintain a min-heap of exactly size k. The heap's top (minimum) is always the k-th largest element seen so far — because there are exactly k-1 elements larger than it in the heap. On each add: push to heap, then if heap size > k, pop the minimum (too small to be in top-k).

```cpp
class KthLargest {
    priority_queue<int, vector<int>, greater<int>> minHeap; // min-heap
    int k;
public:
    KthLargest(int k, vector<int>& nums) : k(k) {
        for (int n : nums) add(n);
    }

    int add(int val) {
        minHeap.push(val);
        if ((int)minHeap.size() > k)
            minHeap.pop();              // evict smallest; heap stays size k
        return minHeap.top();           // top = k-th largest
    }
};
```

---

## 783. Minimum Distance Between BST Nodes
🔗 [LeetCode](https://leetcode.com/problems/minimum-distance-between-bst-nodes)

**Logic:** Identical approach to #530. Inorder traversal gives sorted order; minimum difference is always between adjacent inorder values. Compare each node with the previous one in the traversal.

```cpp
class Solution {
    int prev = -1, minDiff = INT_MAX;
public:
    int minDiffInBST(TreeNode* root) {
        inorder(root);
        return minDiff;
    }

    void inorder(TreeNode* node) {
        if (!node) return;
        inorder(node->left);
        if (prev != -1)
            minDiff = min(minDiff, node->val - prev);
        prev = node->val;
        inorder(node->right);
    }
};
```

---

## 872. Leaf-Similar Trees
🔗 [LeetCode](https://leetcode.com/problems/leaf-similar-trees)

**Logic:** Collect the leaf values of each tree in left-to-right DFS order into a vector. Two trees are leaf-similar if and only if their leaf sequences are identical.

```cpp
class Solution {
public:
    bool leafSimilar(TreeNode* root1, TreeNode* root2) {
        vector<int> leaves1, leaves2;
        getLeaves(root1, leaves1);
        getLeaves(root2, leaves2);
        return leaves1 == leaves2;
    }

    void getLeaves(TreeNode* node, vector<int>& leaves) {
        if (!node) return;
        if (!node->left && !node->right) {   // leaf: record value
            leaves.push_back(node->val);
            return;
        }
        getLeaves(node->left, leaves);
        getLeaves(node->right, leaves);
    }
};
```

---

## 897. Increasing Order Search Tree
🔗 [LeetCode](https://leetcode.com/problems/increasing-order-search-tree)

**Logic:** Inorder traversal of a BST gives sorted order. Re-wire each node as we visit it: set its left to null, connect it as the right child of the previously visited node. Use a dummy head and a `cur` pointer to build the new chain.

```cpp
class Solution {
    TreeNode* cur;
public:
    TreeNode* increasingBST(TreeNode* root) {
        TreeNode* dummy = new TreeNode(0);
        cur = dummy;
        inorder(root);
        return dummy->right;
    }

    void inorder(TreeNode* node) {
        if (!node) return;
        inorder(node->left);
        node->left = nullptr;    // detach left child
        cur->right = node;       // append to growing chain
        cur = node;              // advance the chain pointer
        inorder(node->right);
    }
};
```

---

## 938. Range Sum of BST
🔗 [LeetCode](https://leetcode.com/problems/range-sum-of-bst)

**Logic:** Use BST ordering to prune the search. If node->val <= low, no need to visit the left subtree (all values there are smaller). If node->val >= high, no need to visit right subtree. Only add node's value if it falls within [low, high].

```cpp
class Solution {
public:
    int rangeSumBST(TreeNode* root, int low, int high) {
        if (!root) return 0;
        int sum = (root->val >= low && root->val <= high) ? root->val : 0;
        if (root->val > low)                         // left might have values in range
            sum += rangeSumBST(root->left, low, high);
        if (root->val < high)                        // right might have values in range
            sum += rangeSumBST(root->right, low, high);
        return sum;
    }
};
```

---

## 965. Univalued Binary Tree
🔗 [LeetCode](https://leetcode.com/problems/univalued-binary-tree)

**Logic:** Every node must have the same value as the root. DFS: at each node compare its value to root->val. If any node differs, return false immediately. The root value is captured once and checked against all descendants.

```cpp
class Solution {
public:
    bool isUnivalTree(TreeNode* root) {
        return dfs(root, root->val);
    }

    bool dfs(TreeNode* node, int val) {
        if (!node) return true;
        if (node->val != val) return false;     // mismatch → not univalued
        return dfs(node->left, val) && dfs(node->right, val);
    }
};
```

---

## 993. Cousins in Binary Tree
🔗 [LeetCode](https://leetcode.com/problems/cousins-in-binary-tree)

**Logic:** Two nodes are cousins if they share the same depth but have different parents. BFS naturally gives us depth level by level. At each node, when we enqueue children, record their parent. Once we find both x and y, compare their depth and parent.

```cpp
class Solution {
public:
    bool isCousins(TreeNode* root, int x, int y) {
        TreeNode *xParent = nullptr, *yParent = nullptr;
        int xDepth = -1, yDepth = -1;
        queue<pair<TreeNode*, TreeNode*>> q;  // {node, parent}
        q.push({root, nullptr});
        int depth = 0;
        while (!q.empty()) {
            int sz = q.size();
            for (int i = 0; i < sz; i++) {
                auto [node, parent] = q.front(); q.pop();
                if (node->val == x) { xDepth = depth; xParent = parent; }
                if (node->val == y) { yDepth = depth; yParent = parent; }
                if (node->left)  q.push({node->left,  node});
                if (node->right) q.push({node->right, node});
            }
            depth++;
        }
        return xDepth == yDepth && xParent != yParent; // same depth, different parent
    }
};
```

---

## 1022. Sum of Root To Leaf Binary Numbers
🔗 [LeetCode](https://leetcode.com/problems/sum-of-root-to-leaf-binary-numbers)

**Logic:** Each root-to-leaf path encodes a binary number. As we go deeper, shift the current number left (×2) and OR in the current node's bit. At a leaf, the accumulated number is complete — add it to the total. Passing the current number down avoids any backtracking.

```cpp
class Solution {
public:
    int sumRootToLeaf(TreeNode* root) {
        return dfs(root, 0);
    }

    int dfs(TreeNode* node, int current) {
        if (!node) return 0;
        current = current * 2 + node->val;              // shift left and add current bit
        if (!node->left && !node->right) return current; // leaf: return completed number
        return dfs(node->left, current) + dfs(node->right, current);
    }
};
```

---

## 1379. Find a Corresponding Node of a Binary Tree in a Clone of That Tree
🔗 [LeetCode](https://leetcode.com/problems/find-a-corresponding-node-of-a-binary-tree-in-a-clone-of-that-tree)

**Logic:** Traverse both the original and cloned tree simultaneously using the exact same DFS path. Whenever we find `target` (by pointer identity) in the original tree, the cloned tree's pointer is at the corresponding node — return it.

```cpp
class Solution {
public:
    TreeNode* getTargetCopy(TreeNode* original, TreeNode* cloned, TreeNode* target) {
        if (!original) return nullptr;
        if (original == target) return cloned;          // match by identity → return clone node
        TreeNode* left = getTargetCopy(original->left, cloned->left, target);
        return left ? left : getTargetCopy(original->right, cloned->right, target);
    }
};
```

---

## 1469. Find All The Lonely Nodes
🔗 [LeetCode](https://leetcode.com/problems/find-all-the-lonely-nodes)

**Logic:** A lonely node is a child node with no sibling (its parent has only one child). At each node, if it has only a left child → left is lonely; if only a right child → right is lonely. Both children present → neither is lonely at this level.

```cpp
class Solution {
public:
    vector<int> getLonelyNodes(TreeNode* root) {
        vector<int> result;
        dfs(root, result);
        return result;
    }

    void dfs(TreeNode* node, vector<int>& result) {
        if (!node) return;
        if (node->left && !node->right)     // only left child → left is lonely
            result.push_back(node->left->val);
        if (node->right && !node->left)     // only right child → right is lonely
            result.push_back(node->right->val);
        dfs(node->left, result);
        dfs(node->right, result);
    }
};
```

---

## 2236. Root Equals Sum of Children
🔗 [LeetCode](https://leetcode.com/problems/root-equals-sum-of-children)

**Logic:** The tree is guaranteed to have exactly 3 nodes. Simply check if root's value equals the sum of its two children's values.

```cpp
class Solution {
public:
    bool checkTree(TreeNode* root) {
        return root->val == root->left->val + root->right->val;
    }
};
```

---

## 2331. Evaluate Boolean Binary Tree
🔗 [LeetCode](https://leetcode.com/problems/evaluate-boolean-binary-tree)

**Logic:** Leaf nodes hold boolean values (0=false, 1=true). Internal nodes are operators (2=OR, 3=AND). Evaluate bottom-up: recursively evaluate both children, then apply the operator at the current internal node.

```cpp
class Solution {
public:
    bool evaluateTree(TreeNode* root) {
        if (!root->left && !root->right)    // leaf node: return its boolean value
            return root->val;
        bool l = evaluateTree(root->left);
        bool r = evaluateTree(root->right);
        return root->val == 2 ? l || r : l && r;   // 2=OR, 3=AND
    }
};
```

---

## 2689. Extract Kth Character From The Rope Tree
🔗 [LeetCode](https://leetcode.com/problems/extract-kth-character-from-the-rope-tree)

**Logic:** In a rope tree, internal nodes concatenate their children's strings; leaves hold actual string segments. To find the k-th character without building the full string: compute the size of the left subtree. If k ≤ left_size, the answer is in the left subtree; otherwise subtract left_size from k and go right.

```cpp
class Solution {
public:
    char getKthCharacter(RopeTreeNode* root, int k) {
        while (root) {
            if (root->val != "")               // leaf node
                return root->val[k - 1];
            int leftSize = getSize(root->left);
            if (k <= leftSize)
                root = root->left;             // k-th char is in left subtree
            else {
                k -= leftSize;                 // adjust k relative to right subtree
                root = root->right;
            }
        }
        return ' ';
    }

    int getSize(RopeTreeNode* node) {
        if (!node) return 0;
        if (node->val != "") return node->val.size();   // leaf: its string length
        return getSize(node->left) + getSize(node->right);
    }
};
```

---

## Quick Pattern Reference

| Pattern | Problems |
|---|---|
| Simple DFS recursion | 94, 100, 104, 112, 144, 145, 226, 617, 965 |
| Inorder traversal (BST sorted property) | 501, 530, 783, 897 |
| BFS level-order | 637, 993 |
| Return extra info from recursion | 110, 543, 563 |
| BST search / pruning | 270, 700, 938 |
| Carry state downward (path, flag, current value) | 257, 404, 1022 |
| Two-tree simultaneous traversal | 100, 101, 617, 1379 |
| Min-heap | 703 |
| N-ary tree | 559, 589, 590 |
