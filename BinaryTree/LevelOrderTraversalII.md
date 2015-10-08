##Binary Tree Level Order Traversal II

41% Accepted

	Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

	Have you met this question in a real interview? Yes
	Example
	Given binary tree {3,9,20,#,#,15,7},

	    3
	   / \
	  9  20
	    /  \
	   15   7


	return its bottom-up level order traversal as:

	[
	  [15,7],
	  [9,20],
	  [3]
	]

####Tags Expand
- Queue
- Binary Tree
- Binary Tree Traversal
- Breadth First Search

####思路
- 跟level order遍历一样，只不过使用了add(index,element)直接每次加在最前面

```java
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: Level order a list of lists of integer
     */
    public ArrayList<ArrayList<Integer>> levelOrderBottom(TreeNode root) {
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
            result.add(0,level);

        }

        return result;

    }
}
```
