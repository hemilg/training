# [Problem](https://leetcode.com/problems/) -  ``

## Description

There are several cards arranged in a row, and each card has an associated number of points. The points are given in the integer array `cardPoints`.

In one step, you can take one card from the beginning or from the end of the row. You have to take exactly `k` cards. Your score is the sum of the points of the cards you have taken.

Given the integer array `cardPoints` and the integer `k`, return the maximum score you can obtain.

### Example Input

```
cardPoints = [1, 79, 80, 1, 1, 1, 200, 1], k = 3
```

### Example Output

```
202
```

## Solution 1

```java
class Solution {
    public int maxScore(int[] cardPoints, int k) {
        
        final int windowSize = cardPoints.length - k;
        
        
        int prevSum = 0;   
        for (int i = 0; i < windowSize; i++) {
            prevSum += cardPoints[i];
        }
        
        int totalSum = prevSum;
        int minimum = prevSum;
        for (int i = windowSize; i < cardPoints.length; i++) {
            totalSum += cardPoints[i];
            prevSum += cardPoints[i];
            prevSum -= cardPoints[i - windowSize];
            
            if (prevSum < minimum) {
                minimum = prevSum;
            }
        }
        
        return totalSum - minimum;
    }
}
```
### Time Complexity

- O(N)

### Space Complexity

- O(1)

### Data Structures/Patterns

- Sliding window

### Pros

- 

### Cons

- 