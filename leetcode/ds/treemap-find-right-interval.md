# [Find Right Interval](https://leetcode.com/problems/find-right-interval) -  `Medium`

## Description

You are given an array of intervals, where `intervals[i] = [start_i, end_i]` and each `start_i` is unique.

The right interval for an interval `i` is an interval `j` such that `start_j >= end_i` and `start_j` is minimized.

Return an array of right interval indices for each interval `i`. If no right interval exists for interval `i`, then put -1 at index `i`.

### Example Input

```
[
    [1,4],
    [2,3],
    [3,4]
]
```

### Example Output

```
[-1,2,-1]
```

## Solution 1

```java
class Solution {
    public int[] findRightInterval(int[][] intervals) {
        
        final int n = intervals.length;
        
        // key-sorted map of: start -> [index, end]
        final TreeMap<Integer, List<Integer>> m = new TreeMap<>();
        final int[] output = new int[n];
        
        // populating map for each of n intervals
        for (int i = 0; i < n; i++) {
            final int[] interval = intervals[i];
            final int start = interval[0];
            final int end = interval[1];
            
            // O(log n) - insertion into balanced tree
            m.put(start, List.of(i, end));
        }
        
        // populating output using map for each of n intervals
        for (int i = 0; i < n; i++) {
            final int[] interval = intervals[i];
            final int end = interval[1];
            
            // O(log n) - search in binary tree
            final Map.Entry<Integer, List<Integer>> right = m.higherEntry(end - 1);

            if (right == null) {
                output[i] = -1;
                continue;
            }

            final int rightIndex = right.getValue().get(0);
            output[i] = rightIndex;
        }
        
        return output;
        
    }
}
```
### Time Complexity

- `O(n log n)`

### Space Complexity

- `O(n)`

### Data Structures/Patterns

- `TreeMap`, `TreeMap::higherEntry`

### Pros

- 

### Cons

- 