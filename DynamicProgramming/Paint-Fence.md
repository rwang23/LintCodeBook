##Paint Fence

    Total Accepted: 7437 Total Submissions: 24286 Difficulty: Easy
    There is a fence with n posts, each post can be painted with one of the k colors.

    You have to paint all the posts such that no more than two adjacent fence posts have the same color.

    Return the total number of ways you can paint the fence.

    Note:
    n and k are non-negative integers.

####思路

        state:
        same[i] how many solution when i fences and last two are in same color(i and i - 1)
        diff[i] how many solution when i fences and last two are in diff color(i and i - 1)
        function:
        same[i] = diff[i - 1]
        diff[i] = (diff[i - 1] + same[i - 1]) * (k - 1)
        initialize:
        same[0] = 0
        diff[0] = 1
        answer:
        same[n - 1] + diff[n - 1]


```java
public class Solution {
    public int numWays(int n, int k) {
        if (n <= 0 || k <= 0) {
            return 0;
        }

        int[] same = new int[n];
        int[] diff = new int[n];
        same[0] = 0;
        diff[0] = k;
        for (int i = 1; i < n; i++) {
            same[i] = diff[i - 1];
            diff[i] = (diff[i - 1] + same[i - 1]) * (k - 1);
        }
        return same[n - 1] + diff[n - 1];

    }
}
```

####空间优化
```java
public class Solution {
    public int numWays(int n, int k) {
        if (n <= 0 || k <= 0) {
            return 0;
        }

        int[] same = new int[2];
        int[] diff = new int[2];
        same[0] = 0;
        diff[0] = k;
        for (int i = 1; i < n; i++) {
            same[i % 2] = diff[(i - 1) % 2];
            diff[i % 2] = (diff[(i - 1) % 2] + same[(i - 1) % 2]) * (k - 1);
        }
        return same[(n - 1) % 2] + diff[(n - 1) % 2];

    }
}
```
