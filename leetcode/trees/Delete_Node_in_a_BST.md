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
```

### Complexity

#### Time

#### Space

### Data Structures/Patterns

### Pros

### Cons

### Notes

Gotta get better at identifying which tree problems should be done recursively, and which ones should be done iteratively. Seems like recursive is way nicer for BST. Spent about an hour trying to do this one iterateively, with a `findPathToDeletionNode` and `findPathToMax` private methods. I was on the right track, but it was an uphill battle. this was a clear use case for recursion. Going to try to re-implement [this](https://leetcode.com/problems/delete-node-in-a-bst/discuss/93296/Recursive-Easy-to-Understand-Java-Solution/221001) code from scratch tomorrow.
