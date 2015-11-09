##Jump Game II

34% Accepted

    Given an array of non-negative integers, you are initially positioned at the first index of the array.

    Each element in the array represents your maximum jump length at that position.

    Your goal is to reach the last index in the minimum number of jumps.

    Have you met this question in a real interview? Yes
    Example
    Given array A = [2,3,1,1,4]

    The minimum number of jumps to reach the last index is 2. (Jump 1 step from index 0 to 1, then 3 steps to the last index.)

####Tags Expand
- Greedy
- Array

####思路
- 找到第一个可以跳过的就行了，后面的尽管可以跳过，但是step肯定比第一个跳过的多，所以得到了step就直接break就行
- 设置了steps[i] = Integer.MAX_VALUE; 如果step[i]没改变的话，说明不用这个值就能跳过，也就是说之前有别的数可以跳过

```java
public class Solution {
    public int jump(int[] A) {
        int[] steps = new int[A.length];

        steps[0] = 0;
        for (int i = 1; i < A.length; i++) {
            steps[i] = Integer.MAX_VALUE;
            for (int j = 0; j < i; j++) {
                if (steps[j] != Integer.MAX_VALUE && j + A[j] >= i) {
                    steps[i] = steps[j] + 1;
                    break;
                }
            }
        }

        return steps[A.length - 1];
    }
}

```
####另一种思路
- 从i j 关系去构思

```java
public class Solution {
    public int jump(int[] A) {
        int[] steps = new int[A.length];

        steps[0] = 0;
        for (int i = 1; i < A.length; i++) {
            int min = Integer.MAX_VALUE;
            for (int j = 0; j < i; j++) {
                if (j + A[j] >= i) {
                    min = Math.min(min,steps[j]);
                }
                steps[i] = min + 1;
            }
        }

        return steps[A.length - 1];
    }
}

```
####优化
- 加上贪心思想，遇到第一个就说明是最短路径，break

```java
public class Solution {
    public int jump(int[] A) {
        int[] steps = new int[A.length];

        steps[0] = 0;
        for (int i = 1; i < A.length; i++) {
            for (int j = 0; j < i; j++) {
                if (j + A[j] >= i) {
                    steps[i] = steps[j] + 1;
                    break;
                }

            }
        }

        return steps[A.length - 1];
    }
}

```
