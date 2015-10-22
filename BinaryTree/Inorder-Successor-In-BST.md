##Inorder Successor in BST

27% Accepted

	Given a binary search tree and a node in it,
    find the in-order successor of that node in the BST.

	Have you met this question in a real interview? Yes
	Example
	Given tree = [2,1] and node = 1:

	  2
	 /
	1
	return node 2.

	Given tree = [2,1,3] and node = 2:

	  2
	 / \
	1   3
	return node 3.

	Note
	If the given node has no in-order successor in the tree, return null.

####Challenge
O(h), where h is the height of the BST.

####Tags Expand
- Binary Search Tree
- Binary Tree

###思路
- 重做

####中序遍历的笨办法
- 注意比较p是不是之前的节点的时候不能直接p == pre，而是需要对p和pre的每个子节点的val进行判断是否相等
- O(n)

```java
public class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        // write your code here
        if(root == null){
            return null;
        }
        Stack<TreeNode> stack = new Stack<TreeNode>();

        TreeNode cur = root;
        TreeNode pre = new TreeNode(Integer.MIN_VALUE);
        while(!stack.isEmpty() || cur != null){
            while(cur != null){
                stack.push(cur);
                cur = cur.left;
            }

            cur = stack.peek();
            stack.pop();
            if ( isSameTree(pre,p) ) {
                return cur;
            }
            pre = cur;
            cur = cur.right;
        }
        return cur;
    }
    public boolean isSameTree(TreeNode T1, TreeNode T2) {
        if(T1 == null && T2 == null)
            return true;
        if(T1 == null || T2 == null)
            return false;
        if(T1.val != T2.val)
            return false;
        return isSameTree(T1.left,T2.left) && isSameTree(T1.right, T2.right);
    }
}
```
####简化办法
- O(h)
- [http://www.bubuko.com](http://www.bubuko.com/infodetail-1129057.html)
-　找到的点没有右子树，那么我们就从这个点开始向上找他的父亲节点，在父亲节点中第一个比他大的就是successor（其实就是中序遍历
- 在没有parent指针的情况下，我们就要提前纪录这个第一个比node点大的父亲节点，方法就是，每次root向左边移动的时候就记录这个root，向右边移动则不需要记录，这样就可以记录下这个比它大的最近父节点了。
- 找到的点有右子树，那么就要找他右子树里面的最小点，这个点就是他的successor。
- 特殊情况，没有找到这个点，返回null。

```java
public class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        TreeNode successor = null;
        while (root != null && root.val != p.val) {
            if (root.val > p.val) {
                successor = root;
                root = root.left;
            } else {
                root = root.right;
            }
        }

        if (root == null) {
            return null;
        }

        if (root.right == null) {
            return successor;
        }

        root = root.right;
        // //找右儿子的最小值也就是一直在它右子树第一个根节点一直向左遍历到叶节点
        while (root.left != null) {
            root = root.left;
        }

        return root;
    }
}
```
