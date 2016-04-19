##Create Maximum Number

	Total Accepted: 5378 Total Submissions: 25931 Difficulty: Hard
	Given two arrays of length m and n with digits 0-9 representing two numbers. Create the maximum number of length k <= m + n from digits of the two. The relative order of the digits from the same array must be preserved. Return an array of the k digits. You should try to optimize your time and space complexity.

	Example 1:
	nums1 = [3, 4, 6, 5]
	nums2 = [9, 1, 2, 5, 8, 3]
	k = 5
	return [9, 8, 6, 5, 3]

	Example 2:
	nums1 = [6, 7]
	nums2 = [6, 0, 4]
	k = 5
	return [6, 7, 6, 0, 4]

	Example 3:
	nums1 = [3, 9]
	nums2 = [8, 9]
	k = 3
	return [9, 8, 9]

####思路
- [解法](https://www.hrwhisper.me/leetcode-create-maximum-number/)
- [清晰解释](http://bookshadow.com/weblog/2015/12/24/leetcode-create-maximum-number/)

```
解题思路：
问题可以转化为这样的两个子问题：

1. 从数组nums中挑选出t个数，在保持元素相对顺序不变的情况下，使得选出的子数组最大化。

2. 在保持元素相对顺序不变的前提下，将数组nums1与数组nums2合并，使合并后的数组最大化。
枚举nums1子数组与nums2子数组的长度len1, len2，在满足长度之和len1+len2等于k的前提下，分别求解最大子数组，并进行合并。

然后从合并得到的子数组中取最大数组即为所求。

子问题1的求解：

参考[LeetCode]Remove Duplicate Letters的思路，利用栈保存最大值子数组

时间复杂度为O(n)，其中n为数组的长度。

子问题2的求解：

两数组的合并可以类比归并排序中的merge操作，只不过在选择两数组中较大的元素时，
需要对数组剩余部分的元素进行比较，详见代码。
```
