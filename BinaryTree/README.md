#Binary Tree

- 做二叉树 首先考虑分治法， 根据题目要求，放在左右子树做


###Morris PreOrder Traversal
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
                    pre.right = null;
                    System.out.print(current.data + " ");
                    current = current.right;
                }   /* End of if condition pre->right == NULL */

            } /* End of if condition current->left == NULL*/

        } /* End of while */

    }
```
