##Verify Preorder Sequence in Binary Search Tree
	Total Accepted: 7208 Total Submissions: 19417 Difficulty: Medium
	Given an array of numbers, verify whether it is the correct preorder traversal sequence of a binary search tree.

	You may assume each number in the sequence is unique.

	Follow up:
	Could you do it using only constant space complexity?

####思路
- 可以用递归
- 也可以用stack

####递归
- O(n2)

```java
public class Solution {
    public boolean verifyPreorder(int[] preorder) {
        if (preorder == null || preorder.length <= 1) {
            return true;
        }

        return verifyPreorderHelper(preorder, 0, preorder.length - 1);
    }

    private boolean verifyPreorderHelper(int[] preorder, int lo, int hi) {
        if (lo >= hi) {
            return true;
        }

        int root = preorder[lo];
        int i = lo + 1;
        while (i <= hi && preorder[i] < root) {
            i++;
        }

        int j = i;
        while (j <= hi && preorder[j] > root) {
            j++;
        }

        if (j <= hi) {
            return false;
        }

        return verifyPreorderHelper(preorder, lo + 1, i - 1) &&
               verifyPreorderHelper(preorder, i, hi);
    }
}
```

####Stack
[参考](https://leetcode.com/discuss/51543/java-o-n-and-o-1-extra-space)

```java
public class Solution {
    public boolean verifyPreorder(int[] preorder) {
        if (preorder == null || preorder.length == 0) {
            return true;
        }

        Stack<Integer> stack = new Stack<Integer>();
        int low = Integer.MIN_VALUE;
        for (int x : preorder) {
            if (x <= low) {
                return false;
            }
            while (!stack.isEmpty() && stack.peek() < x) {
                low = stack.pop();
            }
            stack.push(x);
        }

        return true;
    }
}
```
