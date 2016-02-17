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


###难题
 - maximum subarray iii done
 - median of two sorted arrays done

###每天理解
 - quicksort以及partition array 自己在这里经常犯错误
 - trie树
