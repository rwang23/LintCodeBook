##Serialize and Deserialize Binary Tree
Design an algorithm and write code to serialize and deserialize a binary tree. 
Writing the tree to a file is called 'serialization' 
and reading back from the file to reconstruct the exact same binary tree is 'deserialization'.

###Example
  An example of testdata: Binary tree {3,9,20,#,#,15,7}, denote the following structure:

    3
   / \
  9  20
    /  \
   15   7

  Our data serialization use bfs traversal. This is just for when you got wrong answer and want to debug the input.

  You can use other method to do serializaiton and deserialization.

###Notice
  There is no limit of how you deserialize or serialize a binary tree,
  LintCode will take your output of serialize as the input of deserialize, it won't check the result of serialize.

####思路
- 编程string，空节点用#代替
- 在deserialize的时候，下标才是最难的
- 当有子节点是空的时候，i遍历要加上空的数量

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */


public class Solution {
    /**
     * This method will be invoked first, you should design your own algorithm 
     * to serialize a binary tree which denote by a root node to a string which
     * can be easily deserialized by your own "deserialize" method later.
     */
    //serialize的结果{3,9,20,#,#,15,7,#,#,#,#} ， 跟题目说明稍有不一样
    public String serialize(TreeNode root) {
        // write your code here
        if (root == null) {
            return new String("");
        }
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        StringBuilder sb = new StringBuilder();
        sb.append(root.val);
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                
                TreeNode cur = queue.poll();
                sb.append(",");
                if (cur.left != null) {
                    sb.append(cur.left.val);
                    queue.offer(cur.left);
                } else {
                    sb.append("#");
                }
                sb.append(",");
                if (cur.right != null) {
                    sb.append(cur.right.val);
                    queue.offer(cur.right);
                } else {
                    sb.append("#");
                }
            }
        }
        
        return sb.toString();
        
    }

    /**
     * This method will be invoked second, the argument data is what exactly
     * you serialized at method "serialize", that means the data is not given by
     * system, it's given by your own serialize method. So the format of data is
     * designed by yourself, and deserialize it here as you serialize it in 
     * "serialize" method.
     */
    public TreeNode deserialize(String data) {
        // write your code here
        if (data == null || data.length() == 0) {
            return null;
        }
        
        String[] nodes = data.split(",");
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        TreeNode root = new TreeNode(Integer.parseInt(nodes[0]));
        queue.offer(root);
        
        for (int i = 0; i < nodes.length;) {
            
            int size = queue.size();
            //算好下标
            int empty = 0;
            for (int j = 0; j < size; j++) {
                TreeNode cur = queue.poll();
                //此时下标是i+queue里边的父节点的个数，再加上已经使用过的节点数量
                int leftIndex = i + size + 2 * j;
                if (leftIndex < nodes.length) {
                    if (nodes[leftIndex].equals("#")) {
                        cur.left = null;
                        //当子树是空的时候，需要在循环外加上这个空的节点数量，
                        //否则外面的父节点的指引就到了空节点
                        empty++;
                    } else {
                        TreeNode left = new TreeNode(Integer.parseInt(nodes[leftIndex]));
                        cur.left = left;
                        queue.offer(left);
                    }
                }
                
                int rightIndex = i + size + 1 + 2 * j;
                if (rightIndex < nodes.length) {
                    if (nodes[rightIndex].equals("#")) {
                        cur.right = null;
                        empty++;
                    } else {
                        TreeNode right = new TreeNode(Integer.parseInt(nodes[rightIndex]));
                        cur.right = right;
                        queue.offer(right);
                    }
                }
            }
            i = size  + i + empty;
            if (size == 0) {
                break;
            }
        }
        
        return root;
    }
}
```
