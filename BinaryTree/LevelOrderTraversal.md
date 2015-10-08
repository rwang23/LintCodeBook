## Binary Tree Level Order Traversal

32% Accepted

	Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

	Have you met this question in a real interview? Yes
	Example
	Given binary tree {3,9,20,#,#,15,7},

	    3
	   / \
	  9  20
	    /  \
	   15   7


	return its level order traversal as:

	[
	  [3],
	  [9,20],
	  [15,7]
	]

####Challenge
- Challenge 1: Using only 1 queue to implement it.

- Challenge 2: Use DFS algorithm to do it.

####Tags Expand
- Queue
- Binary Tree
- Binary Tree Traversal
- Breadth First Search

----

### 1 Queue Challenge Solution

####思路
- Queue<TreeNode> queue = new LinkedList<TreeNode>(); 否则会报错，因为queue是abstract类型
- Queue集成了Collection, 所以可以使用size()
- 使用queue 进行BFS
- 完成一层，通过size大小判断，然后就可以加入result


```java

public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: Level order a list of lists of integer
     */
    public ArrayList<ArrayList<Integer>> levelOrder(TreeNode root) {
        // write your code here
        if(root == null){
            return new ArrayList<ArrayList<Integer>>();
        }

        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
        Queue<TreeNode> queue = new LinkedList<TreeNode>();

        TreeNode cur = root;
        queue.offer(root);

        while(queue.peek() != null){
            int size = queue.size();
            ArrayList<Integer> level = new ArrayList<Integer>();
            for(int i = 0; i < size; i++){
                cur = queue.peek();
                if(cur.left != null){
                    queue.offer(cur.left);
                }
                if(cur.right != null){
                    queue.offer(cur.right);
                }
                level.add(cur.val);
                queue.poll();
            }
            result.add(level);

        }
        return result;

    }
}

```

----
###DFS Challenge

####思路
- 其实是伪DFS
- 设置maxlevel 限制每一层进入的最大的depth，然后通过分治的思想进行计算

```java
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: Level order a list of lists of integer
     */
    public ArrayList<ArrayList<Integer>> levelOrder(TreeNode root) {
        ArrayList<ArrayList<Integer>> results = new ArrayList<ArrayList<Integer>>();

        if (root == null) {
            return results;
        }

        int maxLevel = 0;
        while (true) {
            ArrayList<Integer> level = new ArrayList<Integer>();
            dfs(root, level, 0, maxLevel);
            if (level.size() == 0) {
                break;
            }

            results.add(level);
            maxLevel++;
        }

        return results;
    }

    private void dfs(TreeNode root,
                     ArrayList<Integer> level,
                     int curtLevel,
                     int maxLevel) {
        if (root == null || curtLevel > maxLevel) {
            return;
        }

        if (curtLevel == maxLevel) {
            level.add(root.val);
            return;
        }

        dfs(root.left, level, curtLevel + 1, maxLevel);
        dfs(root.right, level, curtLevel + 1, maxLevel);
    }
}
```






