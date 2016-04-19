##Two Sum in BST
[geeksforgeeks problem](http://www.geeksforgeeks.org/find-a-pair-with-given-sum-in-bst/)

       8
      /  \
     5    14
    /\    /\
   0  7  10  20
     /   /\
    6   9  12


  target : 15
O(lgn)

/*
left{8}
right{8}
result{5,10}{6, 9}
leftNode 8
rightNode 8
sum = 17 > 15
*/

####思路
- 方法1: in order traversal,因为是BST,所以是已经sorted,所以再用two pointers, Time O(n) Space O(n)
- 方法2: 用stack来记录parent节点,然后先找到最左和最右节点,依次从stack中去出parent来模拟two pointers
- 要注意的地方是走到parent节点后,要再走另一个子节点
- Time O(n) Space(logn)


```java
public class Solution {
    public List<TreeNode> TwoSumBST(TreeNode root, int target) {
        if (root != null) {
            return new ArrayList<TreeNode>();
        }
        List<TreeNode> list = new ArrayList<TreeNode>();
        List<List<TreeNode>> result = new ArrayList<ArrayList<TreeNode>>();
        Stack<TreeNode> left = new Stack<TreeNode>();
        Stack<TreeNode> right = new Stack<TreeNode>();
        TreeNode leftNode = root;
        while (leftNode.left != null) {
            left.push(leftNode);
            leftNode = leftNode.left;
        }

        TreeNode rightNode = root;
        while Two Sum in BSTrightNode.right != null) {
            right.push(rightNode);
            rightNode = rightNode.right;
        }
        while (leftNode != rightNode) {
            if (leftNode.val + rightNode.val == target) {
                list.add(leftNode);
                list.add(rightNode);
                result.add(new ArrayList<TreeNode>(list));
                list.clear();

                if (rightNode.left != null) {
                    rightNode = rightNode.left;
                    while (rightNode.right != null) {
                        rightNode = rightNode.right;
                        right.push(rightNode);
                    }
                } else {
                    rightNode = right.poll();
                }

                if (leftNode.right != null) {
                    leftNode = leftNode.right;
                    while (leftNode.left != null) {
                        leftNode = leftNode.left;
                        left.push(leftNode);
                    }
                } else {
                    leftNode = left.poll();
                }

            } else if (leftNode.val + rightNode.val > target) {
                if (rightNode.left != null) {
                    rightNode = rightNode.left;
                    while (rightNode.right != null) {
                        rightNode = rightNode.right;
                        right.push(rightNode);
                    }
                } else {
                    rightNode = right.poll();
                }
            } else {
                if (leftNode.right != null) {
                    leftNode = leftNode.right;
                    while (leftNode.left != null) {
                        leftNode = leftNode.left;
                        left.push(leftNode);
                    }
                } else {
                    leftNode = left.poll();
                }
            }
        }
        return result;
    }
}
```


