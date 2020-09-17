# [Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/) - `Medium`

## Problem

Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.

### Example Input

```
root = [5,3,6,2,4,null,7]
key = 3

    5
   / \
  3   6
 / \   \
2   4   7
```

### Example Output

Output 1

```
root = [5,4,6,2,null,null,7]

    5
   / \
  4   6
 /     \
2       7
```

Output 2

```
[5,2,6,null,4,null,7].

    5
   / \
  2   6
   \   \
    4   7
```

## Solution

```java
class Solution {
    public TreeNode deleteNode(final TreeNode root, int key) {
        if (root == null) {
            return null;
        }
        
        // Finding removal TreeNode
        
        if (root.val < key) {
            root.right = deleteNode(root.right, key);
            return root;
        }
        
        if (root.val > key) {
            root.left = deleteNode(root.left, key);
            return root;
        }
        
        // TreeNode has zero or one children
        
        if (root.left == null && root.right == null) {
            return null;
        }
        
        if (root.left != null && root.right == null) {
            return root.left;
        }
        
        if (root.left == null && root.right != null) {
            return root.right;
        }
        
        // TreeNode has two children
        
        TreeNode newRoot;
        
        if (root.left.right == null) {
            newRoot = root.left;
        } else {
            newRoot = removeLargest(root.left);
            newRoot.left = root.left;
        }
        
        newRoot.right = root.right;
        return newRoot;
    }
    
    private TreeNode removeLargest(final TreeNode node) {
        TreeNode prev = node;
        TreeNode curr = node.right;
        
        while(curr.right != null) {
            prev = curr;
            curr = curr.right;
        }
        
        prev.right = curr.left;
        curr.left = null;
        return curr;
    }
}
```

### Complexity

#### Time

This algorithm does not visit every node in the tree, but rather visits the nodes between the root and the removal node, and between the removal node and the replacement node. At each node, there is constant `O(1)` work being done, so the time complexity is `O(h)`, where `h` is the height of the tree, a value that ranges from `log n` to `n`, depending on the tree shape.

#### Space

The amount of memory being used within a single stack frame is `O(1)`. When at its deepest, the recursive call stack will follow a path from the root to the deletion node, and from the deletion node to its replacement node, the largest node in its left subtree. This call stack does not exceed the height of the tree, so the memory usage is `O(h)` where `h` is the height of the tree. The value of `h` will range from `log n` to `n`, depending on the tree shape.

### Data Structures/Patterns

- Helper method uses an iterative traversal and tracks the parent node of the maximum node. This is to ensure that we can restore the BST ordering property after the maximum node is removed.
- Traversal to the removal node uses the BST ordering property and the reassigning the return value of the recursive method. This removes the need for tracking the parent node of the removal node, since reassignments will occur 

### Pros

Recursion makes the solution simple and expressive.

### Cons

Recursive overhead, but despite this, recursion is still the way to go.

### Notes

Gotta get better at identifying which tree problems should be done recursively, and which ones should be done iteratively. Seems like recursive is way nicer for BST. Spent about an hour trying to do this one iterateively, with a `findPathToDeletionNode` and `findPathToMax` private methods. I was on the right track, but it was an uphill battle. this was a clear use case for recursion. Going to try to re-implement [this](https://leetcode.com/problems/delete-node-in-a-bst/discuss/93296/Recursive-Easy-to-Understand-Java-Solution/221001) code from scratch tomorrow.

Tomorrow: feeling better about it, was able to get a working solution.
