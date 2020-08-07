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
```

### Complexity

#### Time

#### Space

### Data Structures/Patterns

### Pros

### Cons

### Notes
