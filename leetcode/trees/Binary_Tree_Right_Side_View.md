# [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/) -  `Medium`

## Problem

Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

## Related

[Populating Next Right Pointers In Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)

[Boundary of Binary Tree](https://leetcode.com/problems/boundary-of-binary-tree/)

## Example Input

```
   1
 /   \
2     3
 \     \
  5     4
```

## Example Output

```
[1, 3, 4]
```

---

## Recursive Solution
```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        if (root == null) {
            return new ArrayList<Integer>();
        }
        
        List<Integer> l = rightSideView(root.left);
        List<Integer> r = rightSideView(root.right);

        for (int i = r.size(); i < l.size(); i++) {
            r.add(l.get(i));
        }

        r.add(0, root.val);
        return r;
    }
}
```
### Stats

| Metric | Measure | Percentile |
|:---:| :---: | :---: |
| Runtime | 2ms | 21.74% |
| Memory Usage | 39.7 MB | 18.49% |

### Time Complexity

- `O(n log n)`, since every node in the tree is visited, and the work done at each one was of order `log n`

### Space Complexity

- `O(n)`, worst case recursive call stack

### Data Structures/Patterns

---

## Iterative Solution

```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        final List<Integer> output = new ArrayList<>();
        
        if (root != null) {
            final Deque<TreeNode> dfs = new ArrayDeque<>();
            dfs.offerLast(root);

            while (!dfs.isEmpty()) {

                final TreeNode rightMost = dfs.peekFirst();
                output.add(rightMost.val);

                for (int i = dfs.size(); i > 0; i--) {
                    final TreeNode node = dfs.pollFirst();
                    if (node.right != null) {
                        dfs.offerLast(node.right);
                    }
                    if (node.left != null) {
                        dfs.offerLast(node.left);
                    }
                }
            }
        }
        
        return output;
    }
}   
```

### Stats

| Metric | Measure | Percentile |
|:---:| :---: | :---: |
| Runtime | 1ms | 83.24% |
| Memory Usage | 37.8 MB | 95.87% |

### Time Complexity

### Space Complexity

### Data Structures/Patterns

BFS for reverse level order traversal with a Deque, add value of first treeNode in bfs