# [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) -  `Medium`

## Problem

Given an n-ary tree, return the level order traversal of its nodes' values.

### Example Input

Nary-Tree input serialization is represented in their level order traversal, each group of children is separated by the null value (See examples).

root = `[1,null,3,2,4,null,5,6]`

### Example Output

Level order traversal as:
```
[
    [1],
    [3,2,4],
    [5,6]
]
```
## Solution
```java
class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        final List<List<Integer>> output = new ArrayList<List<Integer>>();
        
        if (root == null) {
            return output;
        }
        
        final Queue<Node> dfsQueue = new LinkedList<Node>();
        dfsQueue.offer(root);

        while(!dfsQueue.isEmpty()) {
            final List<Integer> levelList = new ArrayList<Integer>();
            final int levelSize = dfsQueue.size();

            for(int i = 0; i < levelSize; i++) {
                final Node currNode = dfsQueue.poll();
                levelList.add(currNode.val);
                if (currNode.children == null) {
                    continue;
                }
                
                for (final Node child : currNode.children) {
                    if (child != null) {
                        dfsQueue.offer(child);
                    }
                }
            }

            output.add(levelList);
        }
        
        return output;
    }
}
```
### Complexity

#### Time

`O(n)` - every node is visited, and the work done at each node takes constant time.

#### Space

`O(n)` - output list stores all nodes, number of nodes in queue does not exceed `n`

### Data Structures/Patterns

- Queue for DFS traversal
- ArrayList for output list
