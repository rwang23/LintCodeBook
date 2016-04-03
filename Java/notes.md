##一些注意点
- 判断arraylist为空 一种是 arraylist == null(本身为null) 另一种 是isEmpty() (已经创建,但是没有值)
- 普通数组就可以直接 array == null
- int compare(T o1,T o2)
Compares its two arguments for order. Returns a negative integer, zero, or a positive integer as the first argument is less than, equal to, or greater than the second.
- 如果求最大最小值的时候,初始化设置不一定是Integer.MAX_VALUE / MIN_VALUE, 很有可能是数组第一个数字,注意题意,容易粗心

####转化数据类型
	float ratio = diffFrom30 / 30;
	rgb[0] = (int) (255 * ratio);

###重做的题
- inorder successor in bst done
- binary tree path sum done
- subarry sum closest done
- maximum product subarray done
- best time to buy and sell stock iii
- permutations index
- Union Find: find the weak component
- word ladder

###还没完全掌握
 - Unique Binary Search Trees
 - next permutations
 - permutation sequence
 - heap的实现
 - Count of Smaller Numbers After Self没理解
 - Count of Range Sum没理解
 - Morris Traversal

###Leetcode一轮做错的题
- Integer to English Words
- Find the duplicate number
- String to Integer (atoi)
- Restore IP Addresses
- Binary Tree Upside Down
- Verify Preorder Sequence in Binary Search Tree

###Leetcode一轮不会做的题
- First Missing Positive
- Different Ways to Add Parentheses
- Remove Duplicate Letters 不懂
- (http://fujiaozhu.me/?p=772) (http://traceformula.blogspot.com/2015/12/remove-duplicate-letters-leetcode.html) (http://massivealgorithms.blogspot.com/2015/12/leetcode-316-remove-duplicate-letters.html) (http://www.bubuko.com/infodetail-1249912.html)
- Burst Balloons
-

###Leetcode一轮虽然做对,但是花时有点长或者需要注意再重做的题
- Remove Duplicates from Sorted Array I and II
- Word Search II, 特别考DFS里的限制条件,特别棒的题

##总结
####二叉树中做DFS
- 二叉树的 DFS 跟其他的通常有点不一样,
- 其他DFS 一般在list里边加入了一个数,后来回溯的时候会再删除掉
- 然后二叉树DFS一般不用回溯,所以不用删除,这样导致传递的arraylist其实指向的是一个
- 所以每次递归中要声明一个新的arraylist,这样才不会错误
- 参见binary tree path sum II

####条件表达式
- 条件表达式一定要用括号,好几次就是这样错误几个运算在一起,也有条件表达式,结果没用括号,并且debug一个小时才发现! 注意注意!
