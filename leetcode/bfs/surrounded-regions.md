# [](https://leetcode.com/problems/) -  ``

## Description

Given a 2D board containing `X`s and `O`s (the letter `O`), capture all regions surrounded by `X`. A region is captured by flipping all `O`s into `X`s in that surrounded region.

### Example Input

```
X X X X
X O O X
X X O X
X O X X
```

### Example Output

```
X X X X
X X X X
X X X X
X O X X
```

## Solution 1

```java
class Solution {
    public void solve(char[][] board) {
        if (board.length <= 2 || board[0].length <= 2) {
            return;
        }

        final int numCols = board[0].length;
        final int numRows = board.length;

        final Deque<List<Integer>> bfs = new ArrayDeque<>();

        // O(sqrt n), horizontal borders
        IntStream.range(0, numCols)
            .forEach(j -> {
                if (board[0][j] == 'O') {
                    bfs.offerLast(List.of(0, j));
                }

                if (board[numRows - 1][j] == 'O') {
                    bfs.offerLast(List.of(numRows - 1, j));
                }
            });

        // O(sqrt n), vertical borders
        IntStream.range(1, numRows - 1)
            .forEach(i -> {
                if (board[i][0] == 'O') {
                    bfs.offerLast(List.of(i, 0));
                }

                if (board[i][numCols - 1] == 'O') {
                    bfs.offerLast(List.of(i, numCols - 1));
                }
            });

        final Set<List<Integer>> noFlip = new HashSet<>(bfs);

        while (!bfs.isEmpty()) {
            for (int k = bfs.size(); k > 0; k--) {
                final List<Integer> currPosition = bfs.pollFirst();
                final List<Integer> u = List.of(currPosition.get(0) - 1, currPosition.get(1));
                final List<Integer> d = List.of(currPosition.get(0) + 1, currPosition.get(1));
                final List<Integer> l = List.of(currPosition.get(0), currPosition.get(1) - 1);
                final List<Integer> r = List.of(currPosition.get(0), currPosition.get(1) + 1);

                Stream.of(u, d, l, r)
                    .forEach(x -> {
                        final int row = x.get(0);
                        final int col = x.get(1);

                        if (0 <= row && row < numRows &&
                            0 <= col && col < numCols &&
                            board[row][col] == 'O' &&
                            noFlip.add(x)) {
                                bfs.offerLast(x);
                        }
                    });
            }
        }

        // O(N^2) - Iterate through inner board, flip any o whose position is not marked as noFlip
        for (int i = 1; i < board.length - 1; i++) {
            for (int j = 1; j < board[0].length - 1; j++) {
                if (board[i][j] == 'O') {
                    if (noFlip.contains(List.of(i, j))) {
                        continue;
                    } else {
                        board[i][j] = 'X';
                    }
                }
            }
        }
    }
}
```
### Time Complexity

- O(N), all grid locations are visited

### Space Complexity

- 

### Data Structures/Patterns

- 

### Pros

- 

### Cons

- 