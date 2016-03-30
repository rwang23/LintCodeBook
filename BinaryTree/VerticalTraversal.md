##Vertical Traversal

Given a binary tree, print it vertically. The following example illustrates vertical order traversal.
           1
        /    \
       2      3
      / \    / \
     4   5  6   7
             \   \
              8   9


The output of print this tree vertically will be:
4
2
1 5 6
3 8
7
9


####思路
- 存position,
- root是0, root.left 是 -1, root.right 是1
- 依次类推

```
                 0
              /    \
             -1      1
            / \    / \
          -2   0  0   2
                   \   \
                    1   3

      1 2  3 4 5 6 7 8 9
      0 -1 1 -2
      -2 -1 -1 0 1 2 3 4
      4 2 1 5 6 3 8 7 9
```

```java
public class Solution {

    public void verticalTraversal(TreeNode root) {
        if (root == null) {
            return;
        }

        Map<TreeNode, Integer> map = new HashMap<TreeNode, Integer>();
        preorder(root, map, 0);
        for (Map.Entry<TreeNode, Integer> : map.entrySet()) {
            TreeNode key = map.getKey();
            int position = map.get(Value);
        }


    }

    public void preorder(TreeNode root,  Map<TreeNode, Integer> map, int position) {
        if (root == null) {
            return;
        }

        map.aadd(root, position);
        preorder(root.left, map, position - 1);
        preorder(root.right, map, position + 1);

    }
}
```
