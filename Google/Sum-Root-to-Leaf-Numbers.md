##Sum Root to Leaf Numbers

	Total Accepted: 70362 Total Submissions: 219133 Difficulty: Medium
	Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.

	An example is the root-to-leaf path 1->2->3 which represents the number 123.

	Find the total sum of all root-to-leaf numbers.

	For example,

	    1
	   / \
	  2   3
	The root-to-leaf path 1->2 represents the number 12.
	The root-to-leaf path 1->3 represents the number 13.

	Return the sum = 12 + 13 = 25.

####思路
- 最后收工的时候一定要注意用test case来验证
- 这道题dfs里最开始写的是 如果 root == null 才开始计算,这样子就算重了,
- 所以拆开来发现 左右都没子树才开始计算,同时如果一来就是null,那就直接返回

```java

public class Solution {
    int sum = 0;
    public int sumNumbers(TreeNode root) {
        if (root == null) {
            return 0;
        }

        dfs(root, 0);
        return sum;
    }

    public void dfs(TreeNode root, int curVal) {
        if (root == null) {
            return;
        }

        curVal = curVal * 10 + root.val;
        if (root.left == null && root.right == null) {
            sum += curVal;
            return;
        }

        dfs(root.left, curVal);
        dfs(root.right, curVal);
    }
}
```
