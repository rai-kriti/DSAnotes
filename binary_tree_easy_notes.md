# Binary Tree Easy LeetCode — Notes & Solutions (Python)

> All solutions use Python. TreeNode definition assumed:
> ```python
> class TreeNode:
>     def __init__(self, val=0, left=None, right=None):
>         self.val = val; self.left = left; self.right = right
> ```

---

## 94. Binary Tree Inorder Traversal
**Logic:** Inorder = Left → Root → Right. Recursion naturally captures this. Iterative: use a stack — go as far left as possible, pop & record, then move right.

```python
def inorderTraversal(root):
    result = []
    def dfs(node):
        if not node: return
        dfs(node.left)       # visit left subtree first
        result.append(node.val)  # record root
        dfs(node.right)      # visit right subtree last
    dfs(root)
    return result
```

---

## 100. Same Tree
**Logic:** Two trees are same if their roots match AND their left subtrees match AND right subtrees match. Base cases: both None → True; one None → False.

```python
def isSameTree(p, q):
    if not p and not q: return True          # both empty → same
    if not p or not q: return False          # one empty → different
    if p.val != q.val: return False          # values differ → different
    return isSameTree(p.left, q.left) and isSameTree(p.right, q.right)
```

---

## 101. Symmetric Tree
**Logic:** A tree is symmetric if the left subtree is a mirror of the right. Write a helper `isMirror(l, r)` that checks: values match, l.left mirrors r.right, l.right mirrors r.left.

```python
def isSymmetric(root):
    def isMirror(l, r):
        if not l and not r: return True
        if not l or not r: return False
        return (l.val == r.val and
                isMirror(l.left, r.right) and   # outer pair
                isMirror(l.right, r.left))        # inner pair
    return isMirror(root.left, root.right)
```

---

## 104. Maximum Depth of Binary Tree
**Logic:** Depth of a node = 1 + max(depth of left child, depth of right child). Base case: None → 0. The recursion naturally bubbles up the max depth.

```python
def maxDepth(root):
    if not root: return 0
    return 1 + max(maxDepth(root.left), maxDepth(root.right))
```

---

## 108. Convert Sorted Array to Binary Search Tree
**Logic:** To make a height-balanced BST from a sorted array, always pick the middle element as root (this balances left/right counts), recurse on left half → left child, right half → right child.

```python
def sortedArrayToBST(nums):
    if not nums: return None
    mid = len(nums) // 2
    root = TreeNode(nums[mid])              # middle becomes root
    root.left = sortedArrayToBST(nums[:mid])      # left half → left subtree
    root.right = sortedArrayToBST(nums[mid+1:])   # right half → right subtree
    return root
```

---

## 110. Balanced Binary Tree
**Logic:** A tree is balanced if for every node, |height(left) - height(right)| ≤ 1. Use a helper that returns height or -1 if unbalanced. If either child is -1, propagate -1 up immediately (short-circuit).

```python
def isBalanced(root):
    def height(node):
        if not node: return 0
        lh = height(node.left)
        if lh == -1: return -1              # left subtree unbalanced
        rh = height(node.right)
        if rh == -1: return -1              # right subtree unbalanced
        if abs(lh - rh) > 1: return -1     # current node unbalanced
        return 1 + max(lh, rh)
    return height(root) != -1
```

---

## 111. Minimum Depth of Binary Tree
**Logic:** Min depth = shortest path from root to a leaf. IMPORTANT: if a node has only one child, you can't count the empty child side as a leaf path — recurse only on the existing child. Both children present → take min.

```python
def minDepth(root):
    if not root: return 0
    if not root.left: return 1 + minDepth(root.right)   # only right child exists
    if not root.right: return 1 + minDepth(root.left)   # only left child exists
    return 1 + min(minDepth(root.left), minDepth(root.right))
```

---

## 112. Path Sum
**Logic:** At each node, subtract node's value from target. If we hit a leaf and remaining target == 0, a valid path exists. Key: check leaf condition (both children None) before recursing, else we'd count internal nodes as leaves.

```python
def hasPathSum(root, targetSum):
    if not root: return False
    targetSum -= root.val                      # consume current node's value
    if not root.left and not root.right:       # leaf node
        return targetSum == 0
    return hasPathSum(root.left, targetSum) or hasPathSum(root.right, targetSum)
```

---

## 144. Binary Tree Preorder Traversal
**Logic:** Preorder = Root → Left → Right. Record the node first, then recurse left, then right.

```python
def preorderTraversal(root):
    result = []
    def dfs(node):
        if not node: return
        result.append(node.val)   # record root FIRST
        dfs(node.left)
        dfs(node.right)
    dfs(root)
    return result
```

---

## 145. Binary Tree Postorder Traversal
**Logic:** Postorder = Left → Right → Root. Record node LAST after both children processed.

```python
def postorderTraversal(root):
    result = []
    def dfs(node):
        if not node: return
        dfs(node.left)
        dfs(node.right)
        result.append(node.val)   # record root LAST
    dfs(root)
    return result
```

---

## 222. Count Complete Tree Nodes
**Logic:** Naive: count all nodes O(n). Optimized for complete tree: measure left-most depth and right-most depth. If equal, left subtree is perfect → left count = 2^h - 1, recurse only on right. Else right subtree is perfect at h-1 → recurse only on left. O(log²n).

```python
def countNodes(root):
    if not root: return 0
    lh = rh = 0
    l, r = root, root
    while l: lh += 1; l = l.left       # leftmost depth
    while r: rh += 1; r = r.right      # rightmost depth
    if lh == rh:
        return (1 << lh) - 1           # perfect tree: 2^h - 1
    return 1 + countNodes(root.left) + countNodes(root.right)
```

---

## 226. Invert Binary Tree
**Logic:** Swap left and right children at every node. Do this recursively bottom-up or top-down — both work. After swapping, recurse into the (now swapped) children.

```python
def invertTree(root):
    if not root: return None
    root.left, root.right = root.right, root.left   # swap children
    invertTree(root.left)
    invertTree(root.right)
    return root
```

---

## 257. Binary Tree Paths
**Logic:** DFS, carry the current path string. At each node append its value. At a leaf, add the complete path to results. Pass path down as a parameter, not a global, to avoid backtracking issues.

```python
def binaryTreePaths(root):
    result = []
    def dfs(node, path):
        if not node: return
        path += str(node.val)
        if not node.left and not node.right:   # leaf: save path
            result.append(path)
        else:
            dfs(node.left, path + "->")
            dfs(node.right, path + "->")
    dfs(root, "")
    return result
```

---

## 270. Closest Binary Search Tree Value
**Logic:** Leverage BST property. At each node compare current node's value with target. Track closest so far. If target < node.val go left, else go right. This is O(h) instead of O(n).

```python
def closestValue(root, target):
    closest = root.val
    while root:
        if abs(root.val - target) < abs(closest - target):
            closest = root.val           # update closest
        root = root.left if target < root.val else root.right
    return closest
```

---

## 404. Sum of Left Leaves
**Logic:** We need to know if a node is a "left" child — so pass a boolean flag `is_left`. At each leaf, add its value only if `is_left` is True. Non-leaves contribute nothing directly.

```python
def sumOfLeftLeaves(root):
    def dfs(node, is_left):
        if not node: return 0
        if not node.left and not node.right:   # leaf
            return node.val if is_left else 0
        return dfs(node.left, True) + dfs(node.right, False)
    return dfs(root, False)
```

---

## 501. Find Mode in Binary Search Tree
**Logic:** Inorder traversal of BST gives sorted order. Track previous value, current streak count, and max streak. When streak equals max, add to result; when it exceeds max, reset result.

```python
def findMode(root):
    result, prev, count, max_count = [], [None], [0], [0]
    def inorder(node):
        if not node: return
        inorder(node.left)
        count[0] = count[0] + 1 if node.val == prev[0] else 1
        prev[0] = node.val
        if count[0] > max_count[0]:
            max_count[0] = count[0]; result.clear(); result.append(node.val)
        elif count[0] == max_count[0]:
            result.append(node.val)
        inorder(node.right)
    inorder(root)
    return result
```

---

## 530. Minimum Absolute Difference in BST
**Logic:** Inorder traversal yields sorted values. Min difference always occurs between consecutive values in sorted order. Track previous node's value and update min diff as we go.

```python
def getMinimumDifference(root):
    prev, min_diff = [None], [float('inf')]
    def inorder(node):
        if not node: return
        inorder(node.left)
        if prev[0] is not None:
            min_diff[0] = min(min_diff[0], node.val - prev[0])
        prev[0] = node.val
        inorder(node.right)
    inorder(root)
    return min_diff[0]
```

---

## 543. Diameter of Binary Tree
**Logic:** Diameter through a node = left_height + right_height (number of edges). The answer might not pass through root, so track a global max. Return heights up the recursion but update max diameter at each node.

```python
def diameterOfBinaryTree(root):
    max_d = [0]
    def height(node):
        if not node: return 0
        lh = height(node.left)
        rh = height(node.right)
        max_d[0] = max(max_d[0], lh + rh)   # diameter through this node
        return 1 + max(lh, rh)
    height(root)
    return max_d[0]
```

---

## 559. Maximum Depth of N-ary Tree
**Logic:** Same idea as #104 but node can have multiple children. Take max depth among all children and add 1.

```python
def maxDepth(root):
    if not root: return 0
    if not root.children: return 1
    return 1 + max(maxDepth(child) for child in root.children)
```

---

## 563. Binary Tree Tilt
**Logic:** Tilt of a node = |sum of left subtree - sum of right subtree|. We need subtree sums anyway for the calculation, so return subtree sum from recursion and accumulate tilt in a global.

```python
def findTilt(root):
    total_tilt = [0]
    def subtree_sum(node):
        if not node: return 0
        l = subtree_sum(node.left)
        r = subtree_sum(node.right)
        total_tilt[0] += abs(l - r)    # add this node's tilt
        return node.val + l + r        # return total subtree sum
    subtree_sum(root)
    return total_tilt[0]
```

---

## 572. Subtree of Another Tree
**Logic:** For each node in the main tree, check if the subtree rooted there equals `subRoot` using isSameTree. If yes, return True. This is O(m*n) but acceptable for easy level.

```python
def isSubtree(root, subRoot):
    def isSame(s, t):
        if not s and not t: return True
        if not s or not t: return False
        return s.val == t.val and isSame(s.left, t.left) and isSame(s.right, t.right)
    
    if not root: return False
    if isSame(root, subRoot): return True      # match at current root
    return isSubtree(root.left, subRoot) or isSubtree(root.right, subRoot)
```

---

## 589. N-ary Tree Preorder Traversal
**Logic:** Preorder for N-ary: record node, then recurse on each child in order.

```python
def preorder(root):
    result = []
    def dfs(node):
        if not node: return
        result.append(node.val)
        for child in node.children:
            dfs(child)
    dfs(root)
    return result
```

---

## 590. N-ary Tree Postorder Traversal
**Logic:** Postorder for N-ary: recurse all children first, then record node.

```python
def postorder(root):
    result = []
    def dfs(node):
        if not node: return
        for child in node.children:
            dfs(child)
        result.append(node.val)
    dfs(root)
    return result
```

---

## 617. Merge Two Binary Trees
**Logic:** Walk both trees simultaneously. If one is None, return the other (no merging needed). If both exist, add their values and recurse on children.

```python
def mergeTrees(root1, root2):
    if not root1: return root2    # nothing from root1 → use root2 as-is
    if not root2: return root1    # nothing from root2 → use root1 as-is
    root1.val += root2.val        # merge values
    root1.left = mergeTrees(root1.left, root2.left)
    root1.right = mergeTrees(root1.right, root2.right)
    return root1
```

---

## 637. Average of Levels in Binary Tree
**Logic:** BFS level-order traversal. At each level, sum all node values and divide by count. Use a queue; after processing all nodes of a level, compute the average.

```python
from collections import deque
def averageOfLevels(root):
    result, queue = [], deque([root])
    while queue:
        level_sum, level_count = 0, len(queue)
        for _ in range(level_count):
            node = queue.popleft()
            level_sum += node.val
            if node.left: queue.append(node.left)
            if node.right: queue.append(node.right)
        result.append(level_sum / level_count)
    return result
```

---

## 653. Two Sum IV - Input is a BST
**Logic:** Collect all values via inorder traversal into a set. Then for each node check if (k - node.val) exists in the set. Alternatively: traverse and use a seen set inline.

```python
def findTarget(root, k):
    seen = set()
    def dfs(node):
        if not node: return False
        if k - node.val in seen: return True   # complement already seen
        seen.add(node.val)
        return dfs(node.left) or dfs(node.right)
    return dfs(root)
```

---

## 671. Second Minimum Node In a Binary Tree
**Logic:** Special tree: root has exactly 2 children, and root.val = min(left, right). The min value is always root.val. Search for the smallest value strictly greater than root.val across all nodes.

```python
def findSecondMinimumValue(root):
    min_val = root.val
    second = [float('inf')]
    def dfs(node):
        if not node: return
        if min_val < node.val < second[0]:
            second[0] = node.val         # found a better second minimum
        elif node.val == min_val:        # might find second deeper
            dfs(node.left); dfs(node.right)
    dfs(root)
    return second[0] if second[0] < float('inf') else -1
```

---

## 700. Search in a Binary Search Tree
**Logic:** BST property: left < root < right. If val < root.val go left; if val > root.val go right; if equal, return current node. O(h) time.

```python
def searchBST(root, val):
    if not root: return None
    if root.val == val: return root
    if val < root.val: return searchBST(root.left, val)
    return searchBST(root.right, val)
```

---

## 703. Kth Largest Element in a Stream
**Logic:** Maintain a min-heap of size k. The heap's minimum is always the k-th largest element seen so far. On each add: push to heap, pop if size > k.

```python
import heapq
class KthLargest:
    def __init__(self, k, nums):
        self.k = k
        self.heap = []
        for n in nums:
            self.add(n)

    def add(self, val):
        heapq.heappush(self.heap, val)
        if len(self.heap) > self.k:
            heapq.heappop(self.heap)     # remove smallest, keep only top-k
        return self.heap[0]              # smallest in heap = k-th largest overall
```

---

## 783. Minimum Distance Between BST Nodes
**Logic:** Same as #530 — inorder traversal gives sorted values; min difference is between adjacent values.

```python
def minDiffInBST(root):
    prev, min_diff = [None], [float('inf')]
    def inorder(node):
        if not node: return
        inorder(node.left)
        if prev[0] is not None:
            min_diff[0] = min(min_diff[0], node.val - prev[0])
        prev[0] = node.val
        inorder(node.right)
    inorder(root)
    return min_diff[0]
```

---

## 872. Leaf-Similar Trees
**Logic:** Collect the leaf sequence (left to right) of each tree via DFS. Two trees are leaf-similar if their leaf sequences are identical.

```python
def leafSimilar(root1, root2):
    def get_leaves(node):
        if not node: return []
        if not node.left and not node.right: return [node.val]   # leaf
        return get_leaves(node.left) + get_leaves(node.right)
    return get_leaves(root1) == get_leaves(root2)
```

---

## 897. Increasing Order Search Tree
**Logic:** Inorder traversal of BST gives sorted order. Re-link nodes in that order as a right-skewed tree (each node's left = None, right = next node). Use a dummy head and a current pointer.

```python
def increasingBST(root):
    dummy = cur = TreeNode(0)
    def inorder(node):
        nonlocal cur
        if not node: return
        inorder(node.left)
        node.left = None          # detach left
        cur.right = node          # link to chain
        cur = node                # advance pointer
        inorder(node.right)
    inorder(root)
    return dummy.right
```

---

## 938. Range Sum of BST
**Logic:** Use BST property to prune. If node.val < low, no need to check left subtree. If node.val > high, no need to check right subtree. Add node's value only if it's in [low, high].

```python
def rangeSumBST(root, low, high):
    if not root: return 0
    total = root.val if low <= root.val <= high else 0
    if root.val > low:    # left subtree might have values in range
        total += rangeSumBST(root.left, low, high)
    if root.val < high:   # right subtree might have values in range
        total += rangeSumBST(root.right, low, high)
    return total
```

---

## 965. Univalued Binary Tree
**Logic:** A tree is univalued if every node has the same value as the root. DFS: at each node check if its value matches root's value. If any mismatch found, return False.

```python
def isUnivalTree(root):
    def dfs(node):
        if not node: return True
        if node.val != root.val: return False    # mismatch with root value
        return dfs(node.left) and dfs(node.right)
    return dfs(root)
```

---

## 993. Cousins in Binary Tree
**Logic:** Two nodes are cousins if they have the same depth but different parents. BFS level by level: at each node, record (parent, depth) for x and y. After BFS, check same depth, different parent.

```python
def isCousins(root, x, y):
    from collections import deque
    queue = deque([(root, None, 0)])
    info = {}                                    # val → (parent, depth)
    while queue:
        node, parent, depth = queue.popleft()
        if node.val in (x, y):
            info[node.val] = (parent, depth)
        if node.left: queue.append((node.left, node, depth+1))
        if node.right: queue.append((node.right, node, depth+1))
    return (info[x][1] == info[y][1] and         # same depth
            info[x][0] != info[y][0])             # different parent
```

---

## 1022. Sum of Root To Leaf Binary Numbers
**Logic:** Each root-to-leaf path represents a binary number. As we go deeper, shift current number left (multiply by 2) and add current node's bit. At a leaf, add that number to total.

```python
def sumRootToLeaf(root):
    total = [0]
    def dfs(node, current):
        if not node: return
        current = current * 2 + node.val       # shift left and add bit
        if not node.left and not node.right:   # leaf: add binary number
            total[0] += current
        dfs(node.left, current)
        dfs(node.right, current)
    dfs(root, 0)
    return total[0]
```

---

## 1379. Find Corresponding Node in Clone of Tree
**Logic:** Traverse both original and cloned tree simultaneously with the same DFS path. When we find `target` in the original, the cloned tree's pointer is at the corresponding node.

```python
def getTargetCopy(original, cloned, target):
    if not original: return None
    if original is target: return cloned       # found in original → return clone's node
    left = getTargetCopy(original.left, cloned.left, target)
    return left if left else getTargetCopy(original.right, cloned.right, target)
```

---

## 1469. Find All The Lonely Nodes
**Logic:** A lonely node is a node that is the only child (its sibling doesn't exist). At each node with children, check if both children exist — if not, the existing child is lonely. Collect via DFS.

```python
def getLonelyNodes(root):
    result = []
    def dfs(node):
        if not node: return
        if node.left and not node.right:    # right missing → left is lonely
            result.append(node.left.val)
        if node.right and not node.left:    # left missing → right is lonely
            result.append(node.right.val)
        dfs(node.left); dfs(node.right)
    dfs(root)
    return result
```

---

## 2236. Root Equals Sum of Children
**Logic:** Simple: just check root.val == root.left.val + root.right.val (guaranteed 3 nodes).

```python
def checkTree(root):
    return root.val == root.left.val + root.right.val
```

---

## 2331. Evaluate Boolean Binary Tree
**Logic:** Leaves are 0 (False) or 1 (True). Internal nodes are 2 (OR) or 3 (AND). Recursively evaluate children, then apply the operator at the internal node.

```python
def evaluateTree(root):
    if not root.left and not root.right:   # leaf
        return bool(root.val)
    l = evaluateTree(root.left)
    r = evaluateTree(root.right)
    return l or r if root.val == 2 else l and r   # 2=OR, 3=AND
```

---

## 2689. Extract Kth Character From The Rope Tree
**Logic:** Each internal node's string = left_string + right_string. We need k-th character. Use size of left subtree: if k <= left_size, go left; else k -= left_size, go right. Leaf: return leaf.val[k-1].

```python
def getKthCharacter(root, k):
    def size(node):
        if not node: return 0
        if isinstance(node.val, str): return len(node.val)   # leaf
        return size(node.left) + size(node.right)
    
    while root:
        if isinstance(root.val, str):      # leaf node
            return root.val[k - 1]
        left_size = size(root.left)
        if k <= left_size:
            root = root.left              # k-th char is in left subtree
        else:
            k -= left_size               # adjust k and go right
            root = root.right
```

---

## Quick Pattern Reference

| Pattern | Problems |
|---|---|
| Simple DFS recursion | 94, 100, 104, 112, 144, 145, 226, 617, 965 |
| Inorder traversal (BST sorted property) | 530, 783, 897, 501 |
| BFS level-order | 637, 993 |
| Return extra info from recursion | 110, 543, 563 |
| BST search (left/right pruning) | 270, 700, 938 |
| Carry state down (path, flag) | 257, 404, 1022 |
| Two-tree simultaneous traversal | 100, 101, 617, 1379 |
| Min-heap | 703 |
