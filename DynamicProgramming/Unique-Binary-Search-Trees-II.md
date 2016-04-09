##Unique Binary Search Trees II

	Total Accepted: 53220 Total Submissions: 183884 Difficulty: Medium
	Given n, generate all structurally unique BST's (binary search trees) that store values 1...n.

	For example,
	Given n = 3, your program should return all 5 unique BST's shown below.

	   1         3     3      2      1
	    \       /     /      / \      \
	     3     2     1      1   3      2
	    /     /       \                 \
	   2     1         2                 3
	confused what "{1,#,2,3}" means? > read more on how binary tree is serialized on OJ.

####思路
- 求所有,所以一来思路就想到了DFS
- 但是这个DFS有点棘手,
- 一般我们递归是求一个tree,这是要得出list of tree,而且tree又不像数组一样能返回,这个又没有父亲节点,无法返回
- 直接直接构思到了,求出所有所有的合法左节点,所有合法的右结点,然后组装,再附加到result,返回result

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public List<TreeNode> generateTrees(int n) {
        List<TreeNode> result = new ArrayList<TreeNode>();
        if (n <= 0) {
            return result;
        }
        result = dfs(1, n);
        return result;
    }

    public List<TreeNode> dfs(int start, int end) {
        List<TreeNode> result = new ArrayList<TreeNode>();
        if (start > end) {
            result.add(null);
            return result;
        }
        if (start == end) {
            result.add(new TreeNode(start));
            return result;
        }

        for (int i = start; i <= end; i++) {

            List<TreeNode> left = dfs(start, i - 1);
            List<TreeNode> right = dfs(i + 1, end);

            for (int x = 0; x < left.size(); x++) {
                for (int y = 0; y < right.size(); y++) {
                    TreeNode cur = new TreeNode(i);
                    cur.left = left.get(x);
                    cur.right = right.get(y);
                    result.add(cur);
                }
            }
        }
        return result;
    }
}
```
