##Verify Preorder Serialization of a Binary Tree

	Total Accepted: 6286 Total Submissions: 19970 Difficulty: Medium
	One way to serialize a binary tree is to use pre-order traversal. When we encounter a non-null node, we record the node's value. If it is a null node, we record using a sentinel value such as #.

	     _9_
	    /   \
	   3     2
	  / \   / \
	 4   1  #  6
	/ \ / \   / \
	# # # #   # #
	For example, the above binary tree can be serialized to the string "9,3,4,#,#,1,#,#,2,#,6,#,#", where # represents a null node.

	Given a string of comma separated values, verify whether it is a correct preorder traversal serialization of a binary tree. Find an algorithm without reconstructing the tree.

	Each comma separated value in the string must be either an integer or a character '#' representing null pointer.

	You may assume that the input format is always valid, for example it could never contain two consecutive commas such as "1,,3".

	Example 1:
	"9,3,4,#,#,1,#,#,2,#,6,#,#"
	Return true

	Example 2:
	"1,#"
	Return false

	Example 3:
	"9,#,#,1"
	Return false


####思路
####从深度考虑(这个想法其实跟用stack储存父亲节点一样,不过节省了O(h)的stack空间)
- 如果是非null,按照preorder,一定是向下走了一层
- 如果遇到null,一定回到上一层
- 所以depth深度一定在过程中不为零,最后为0

```java
public class Solution {
    public boolean isValidSerialization(String preorder) {
        if (preorder == null || preorder.length() == 0) return false;
        String[] strs = preorder.split(",");
        int depth = 0;
        int i = 0;
        while (i < strs.length - 1) {
            if (strs[i++].equals("#")) {
                if (depth == 0) return false;
                else depth--;
            }
            else depth++;
        }
        if (depth != 0) return false;
        return strs[strs.length - 1].equals("#");
    }
}
```

####从出入度考虑
- [leetcode discuss](https://leetcode.com/discuss/83824/7-lines-easy-java-solution)

```
Some used stack. Some used the depth of a stack.
Here I use a different perspective.
In a binary tree, if we consider null as leaves, then

all non-null node provides 2 outdegree and 1 indegree (2 children and 1 parent),
except root
all null node provides 0 outdegree and 1 indegree (0 child and 1 parent).
Suppose we try to build this tree. During building,
we record the difference between out degree and in degree diff = outdegree - indegree.
When the next node comes, we then decrease diff by 1, because the node provides an in degree.
If the node is not null, we increase diff by 2, because it provides two out degrees.
If a serialization is correct,
diff should never be negative and diff will be zero when finished.
```

```java
public boolean isValidSerialization(String preorder) {
    String[] nodes = preorder.split(",");
    int diff = 1;
    for (String node: nodes) {
        if (--diff < 0) return false;
        if (!node.equals("#")) diff += 2;
    }
    return diff == 0;
}
```
