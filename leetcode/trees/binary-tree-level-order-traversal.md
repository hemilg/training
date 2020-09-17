# [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) -  `Medium`

## Description

Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

### Example Input

Binary tree `[3,9,20,null,null,15,7]`:
```
    3
   / \
  9  20
    /  \
   15   7
```

### Example Output

Level order traversal as:
```
[
  [3],
  [9,20],
  [15,7]
]
```
## Solution 1

```java
class Solution {
    public List<List<Integer>> levelOrder(final TreeNode root) {
        List<List<Integer>> output = new ArrayList<List<Integer>>();
        inorderTraverse(root, 0, output);
        return output;
    }
    
    private void inorderTraverse(final TreeNode root, final int level, final List<List<Integer>> output) {
        if (root != null) {
            
            // Step 1: Get existing list or insert new list and get
            List<Integer> levelList;
            if (output.size() > level) {
                levelList = output.get(level);
            } else {
                levelList = new ArrayList<Integer>();
                output.add(level, levelList);
            }

            // Step 2: add current node value
            levelList.add(root.val);
            
            // Step 3:
            int nextLevel = level + 1;
            inorderTraverse(root.left, nextLevel, output);
            inorderTraverse(root.right, nextLevel, output);
        }
    }
}
```
### Complexity

#### Time

- `ArrayList::add` runs in amortized `O(1)` time
- `ArrayList::get` runs in `O(1)` time
- Ignoring the recursive call, the recursive function's time complexity is `O(1)`
- Recursive function visits every node in the tree, so runtime of traversal is `O(n)`

Total time complexity is `O(1 * n)` = `O(n)`

#### Space

Tree is known to be a binary tree and may not be balanced. The call stack for a recursive function tracks the path from the root to the current node, which is `O(log n)` for the best case (a balanced tree) and `O(n)` for the worst case (a linked list).

### Data Structures/Patterns

- ArrayLists for constant `get()` and `add()` time complexities.
- Recursion for traversal

### Pros

- Simple

### Cons

- Function call overhead with recursion
- Risk of stack overflow with a massive input tree
- Mutating list (more a downside of Java standard library)

## Solution 2

```java
class Solution {
    public List<List<Integer>> levelOrder(final TreeNode root) {
        final List<List<Integer>> answer = new ArrayList<List<Integer>>();
        final Queue<TreeNode> flat = new LinkedList<TreeNode>();
        
        // Use a DFS queue with one node - the root
        if (root != null) {
            flat.offer(root);
        }

        // Each iteration of this loop corresponds to one deeper level in the DFS traversal        
        while (!flat.isEmpty()) {

            final List<Integer> levelList = new ArrayList<Integer>();
            final int currSize = flat.size();
            
            // For each node in this level
            for(int i = 0; i < currSize; i++) {
                final TreeNode node = flat.poll();

                // Add the node to the level's list
                levelList.add(node.val);
                
                // Add its nonnull children to the queue for the next level, starting with left
                final TreeNode left = node.left;
                if (left != null) {
                    flat.offer(left);
                }
                
                final TreeNode right = node.right;
                if (right != null) {
                    flat.offer(right);
                }
            }
            
            answer.add(levelList);
        }
        
        return answer;
    }
}
```

### Complexity

#### Time

- Nested `for` loop along with the `while` loop has the effect of visiting every node, so at least `O(n)`
- `LinkedList::offer` and `LinkedList::poll` are `O(1)` since the linked list tracks head and tail references
- `ArrayList::add` is amortized `O(1)`

#### Space

- At least `O(n)` since we are storing every node in the output list
- Queue takes up `O(1)` space in best case (linked list), and takes up `O(n)` space in worst case (no more than `n/2` in the case of a balanced binary tree)

### Data Structures/Patterns

- LinkedList implementation of Queue for traversal
- ArrayList for quick adding
- DFS mirroring inorder traversal for traversal strategy

### Pros

- Avoid functional overhead of recursion
- No need to index into the output list, so any implementation that supports fast adding would work, even a linked list.

### Cons

- More complex to write