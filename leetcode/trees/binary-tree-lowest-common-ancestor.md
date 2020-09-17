# [Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) - `Medium`

## Problem

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia:
> “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

### Example Test Cases

```
root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1

              3 <- LCA
             / \
            /   \
           /     \
          /       \
         /         \
        /           \
       /             \
 p -> 5               1 <- q
     / \             / \
    /   \           /   \
   /     \         /     \
  6       2       0       8
         / \ 
        7   4

output = 3
```

#### 2

```
root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4

              3
             / \
            /   \
           /     \
          /       \
         /         \
        /           \
       /             \
 p -> 5 <- LCA        1
     / \             / \
    /   \           /   \
   /     \         /     \
  6       2       0       8
         / \ 
        7   4 <- q

output = 5
```

## Solution

```java
class Solution {
    public TreeNode lowestCommonAncestor(final TreeNode root, TreeNode p, TreeNode q) {        
        final Map<TreeNode, TreeNode> parent = new HashMap<TreeNode, TreeNode>();
        final Deque<TreeNode> stack = new ArrayDeque<TreeNode>();
        parent.put(root, null);
        stack.offerLast(root);
        
        // Traverse the tree and store each node's parent until we have
        // processed p and q
        while(!parent.containsKey(q) || !parent.containsKey(p)) {
            final TreeNode node = stack.pollLast();
            if (node.left != null) {
                stack.offerLast(node.left);
                parent.put(node.left, node);
            }
            if (node.right != null) {
                stack.offerLast(node.right);
                parent.put(node.right, node);
            }
        }
        
        
        // Search for the first ancestor of q in a set of ancestors of p
        final Set<TreeNode> pAncestors = new HashSet<TreeNode>();
        
        while(p != null) {
            pAncestors.add(p);
            p = parent.get(p);
        }
        
        while(!pAncestors.contains(q)) {
            q = parent.get(q);
        }
        
        return q;
    }
}
```

### Complexity

#### Time

The first part of the function is a tree traversal that continues until both nodes `p` and `q` are encountered. Thus, this while loop runs in `O(n)` where `n` is the number of nodes in the tree. Inside of this while loop the data structure operations invoked and their costs are:

- `ArrayDeque::push` and `ArrayDeque::pop`, both of which run in amortized `O(1)` time
- `HashMap::put`, which runs in amortized `O(1)` time

Therefore, the first part of the function runs in `O(n)` time.

The second part of the function builds up a set of ancestors of `p`, and traverses through the ancestors of `q` to find the first match. The number of ancestors of any node in a binary tree is no more than `n`, so this second part of the program runs in `O(n)` time as well.

Therefore, the program has time complexity `O(n)`.

#### Space

This solution uses a `Map` which stores at most `n` nodes, a `Deque` that stores at most `n` nodes, and a `Set` that stores at most `n` nodes. Therefore, the space complexity of this solution is `O(n)`.

### Data Structures/Patterns

The `Map` is used to track parents of any nodes that are encountered. This is useful because we can traverse the tree to find any node's children, but tracking the parents becomes necessary whenever upwards traversal is necessary. I was thinking of doing this by maintaining a sequence of nodes over the course of the traversal, but this is made easier by a `Map`.

The `Deque` is used for an iterative depth first traversal of the tree. Java only includes the `Stack` as a vestigial data structure for backwards compatibility, and `Deque` should be used instead. I got confused by using the Queue methods of `poll` and `offer` on the `Deque`, so I should remember to be explicit and use `offerLast` and `pollLast` rather than the queue or stack naming.

The `Set` is used to track ancestors of `p`, and is used to compare against ancestors of `q`. Since we do not need to traverse the set in a sorted order, and only needed to add elements and test membership, we opted to use the `HashSet` implementation instead of a `TreeSet` implementation.

### Pros

- Traversal of the tree ceases after `p` and `q` are both processed
- `HashSet` operations are fast, so adding all ancestors of `p` and checking against ancestors of `q` is a good strategy.

### Cons

### Notes
