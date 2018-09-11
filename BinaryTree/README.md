#Binary Tree
- 做二叉树 首先考虑分治法， 根据题目要求，放在左右子树做


##遍历
- 先序遍历 / 中序遍历 / 后序遍历

###先序遍历（又叫先根遍历、前序遍历）
- 首先访问根结点，然后遍历左子树，最后遍历右子树。遍历左、右子树时，仍按先序遍历。若二叉树为空则返回。
[book](https://rwang23.gitbooks.io/lintcodebook/content/BinaryTree/PreOrderTraversal.html)
###中序遍历（又叫中根遍历）
- 首先遍历左子树，然后访问根结点，最后遍历右子树。遍历左、右子树时，仍按中序遍历。若二叉树为空则返回。简记为左根右。
[book]https://rwang23.gitbooks.io/lintcodebook/content/BinaryTree/InOrderTraversal.html

###后序遍历（又叫后根遍历）
- 首先遍历左子树，然后遍历右子树，最后访问根结点。遍历左、右子树时，仍按后序遍历。若二叉树为空则返回。简记为左右根。
[book](https://rwang23.gitbooks.io/lintcodebook/content/BinaryTree/PostOrderTraversal.html)

[Morris Traversal参考](http://www.cnblogs.com/AnnieKim/archive/2013/06/15/MorrisTraversal.html)

###Morris PreOrder Traversal
	1.If left child is null, print the current node data. Move to right child.
	….Else, Make the right child of the inorder predecessor point to the current node. Two cases arise:
	………a) The right child of the inorder predecessor already points to the current node. Set right child to NULL. Move to right child of current node.
	………b) The right child is NULL. Set it to current node. Print current node’s data and move to left child of current node.
	2...Iterate until current node is not NULL.


```java
    void morrisTraversalPreorder(Node current) {
        while (current != null) {

            // If left child is null, print the current node data. Move to
            // right child.
            if (current.left == null) {
                System.out.print(current.data + " ");
                current = current.right;
            } else {

                // Find inorder predecessor
                Node pre = current.left;
                while (pre.right != null && pre.right != current) {
                    pre = pre.right;
                }

                // If the right child of inorder predecessor already points to
                // this node
                if (pre.right == current) {
                    pre.right = null;
                    current = current.right;
                }

                // If right child doesn't point to this node, then print this
                // node and make right child point to this node
                else {
                    System.out.print(current.data + " ");
                    pre.right = current;
                    current = current.left;
                }
            }
        }
    }
```

###Morris InOrder Traversal
	1. Initialize current as root
	2. While current is not NULL
	   If current does not have left child
	      a) Print current’s data
	      b) Go to the right, i.e., current = current->right
	   Else
	      a) Make current as right child of the rightmost node in current's left subtree
	      b) Go to this left child, i.e., current = current->left

	1. 如果当前节点的左孩子为空，则输出当前节点并将其右孩子作为当前节点。

	2. 如果当前节点的左孩子不为空，在当前节点的左子树中找到当前节点在中序遍历下的前驱节点。

	   a) 如果前驱节点的右孩子为空，将它的右孩子设置为当前节点。当前节点更新为当前节点的左孩子。

	   b) 如果前驱节点的右孩子为当前节点，将它的右孩子重新设为空（恢复树的形状）。输出当前节点。当前节点更新为当前节点的右孩子。

	3. 重复以上1、2直到当前节点为空。

```java
    void MorrisTraversal(Node current) {
        Node pre;

        if (current == null) {
            return;
        }

        while (current != null) {
            if (current.left == null) {
                System.out.print(current.data + " ");
                current = current.right;
            } else {

                /* Find the inorder predecessor of current */
                pre = current.left;
                while (pre.right != null && pre.right != current) {
                    pre = pre.right;
                }

                /* Make current as right child of its inorder predecessor */
                if (pre.right == null) {
                    pre.right = current;
                    current = current.left;
                }

                 /* Revert the changes made in if part to restore the original
                 tree i.e., fix the right child of predecssor */ else {
                 	System.out.print(current.data + " ");
                    pre.right = null;
                    current = current.right;
                }   /* End of if condition pre->right == NULL */

            } /* End of if condition current->left == NULL*/

        } /* End of while */

    }
```
