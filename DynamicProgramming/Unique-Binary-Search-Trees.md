##Unique Binary Search Trees

32% Accepted

	Given n, how many structurally unique BSTs (binary search trees) that store values 1...n?

	Have you met this question in a real interview? Yes
	Example
	Given n = 3, there are a total of 5 unique BST's.

	1           3    3       2      1
	 \         /    /       / \      \
	  3      2     1       1   3      2
	 /      /       \                  \
	2     1          2                  3

####Tags Expand
- Catalan Number
- Dynamic Programming




####思路
[来自水中的鱼](http://fisherlei.blogspot.com/2013/03/leetcode-unique-binary-search-trees.html)
[Leetcode Most Vote](https://leetcode.com/discuss/24282/dp-solution-in-6-lines-with-explanation-f-i-n-g-i-1-g-n-i)



	这题想了好久才想清楚。其实如果把上例的顺序改一下，就可以看出规律了。
	 1                1                      2                       3             3
	    \                 \                 /      \                  /              /
	      3               2              1       3               2             1
	    /                   \                                       /                  \
	 2                       3                                   1                    2

	比如，以1为根的树有几个，完全取决于有二个元素的子树有几种。同理，2为根的子树取决于一个元素的子树有几个。以3为根的情况，则与1相同。

	定义Count[i] 为以[0,i]能产生的Unique Binary Tree的数目，

	如果数组为空，毫无疑问，只有一种BST，即空树，
	Count[0] =1

	如果数组仅有一个元素{1}，只有一种BST，单个节点
	Count[1] = 1

	如果数组有两个元素{1,2}， 那么有如下两种可能
	1                       2
	  \                    /
	    2                1
	Count[2] = Count[0] * Count[1]   (1为根的情况)
	                  + Count[1] * Count[0]  (2为根的情况。

	再看一遍三个元素的数组，可以发现BST的取值方式如下：
	Count[3] = Count[0]*Count[2]  (1为根的情况)
	               + Count[1]*Count[1]  (2为根的情况)
	               + Count[2]*Count[0]  (3为根的情况)

	所以，由此观察，可以得出Count的递推公式为
	Count[i] = ∑ Count[0...k] * [ k+1....i]     0<=k<i-1
	问题至此划归为一维动态规划。



```java
public class Solution {
    /**
     * @paramn n: An integer
     * @return: An integer
     */
    public int numTrees(int n) {
        if (n <= 0) {
            return 1;
        }
        int[] res = new int[n+1];
        res[0] = 1;
        res[1] = 1;
        for(int i=2;i<=n;i++)
        {
            for(int j=0;j<i;j++)
            {
                res[i] += res[j]*res[i-j-1];
            }
        }
        return res[n];
    }
}

```
