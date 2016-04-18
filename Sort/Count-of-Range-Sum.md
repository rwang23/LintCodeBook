##Count of Range Sum
	Total Accepted: 4844 Total Submissions: 18743 Difficulty: Hard
	Given an integer array nums, return the number of range sums that lie in [lower, upper] inclusive.
	Range sum S(i, j) is defined as the sum of the elements in nums between indices i and j (i ≤ j), inclusive.

	Note:
	A naive algorithm of O(n2) is trivial. You MUST do better than that.

	Example:
	Given nums = [-2, 5, -1], lower = -2, upper = 2,
	Return 3.
	The three ranges are : [0, 0], [2, 2], [0, 2] and their respective sums are: -2, -1, 2.

####思路
- naive的方法就是prefixsum, O(n2)完成
- 如果没有负数的话,可以上双指针,但是题目有正数
- 但是不能这么做,题目要求小于O(n2)
- 这道题其实也可以看成Count of Smaller Numbers After Self的变形
- 所以也可以用相类似的方法去做
- [参考](https://leetcode.com/discuss/79083/share-my-solution)

```
count smaller number after self,

count[i] = count of nums[j] - nums[i] < 0 with j > i
Here, after we did the preprocess, we need to solve the problem

count[i] = count of a <= S[j] - S[i] <= b with j > i
ans = sum(count[:])
```

####Merge Sort
- [merge](http://www.qinshaoxuan.com/articles/930.html)


####线段树
- 需要找满足条件 lower ≤ sum[j] – sum[i – 1] ≤ upper ，也就是lower + sum[i – 1] ≤ sum[j] ≤ upper + sum[i – 1]

```java
public class Solution {
    class SegmentTreeNode {
        SegmentTreeNode left;
        SegmentTreeNode right;
        int count;
        long min;
        long max;
        public SegmentTreeNode(long min, long max) {
            this.min = min;
            this.max = max;
        }
    }
    private SegmentTreeNode buildSegmentTree(Long[] valArr, int low, int high) {
        if(low > high) return null;
        SegmentTreeNode stn = new SegmentTreeNode(valArr[low], valArr[high]);
        if(low == high) return stn;
        int mid = (low + high)/2;
        stn.left = buildSegmentTree(valArr, low, mid);
        stn.right = buildSegmentTree(valArr, mid+1, high);
        return stn;
    }
    private void updateSegmentTree(SegmentTreeNode stn, Long val) {
        if(stn == null) return;
        if(val >= stn.min && val <= stn.max) {
            stn.count++;
            updateSegmentTree(stn.left, val);
            updateSegmentTree(stn.right, val);
        }
    }
    private int getCount(SegmentTreeNode stn, long min, long max) {
        if(stn == null) return 0;
        if(min > stn.max || max < stn.min) return 0;
        if(min <= stn.min && max >= stn.max) return stn.count;
        return getCount(stn.left, min, max) + getCount(stn.right, min, max);
    }

    public int countRangeSum(int[] nums, int lower, int upper) {

        if(nums == null || nums.length == 0) return 0;
        int ans = 0;
        Set<Long> valSet = new HashSet<Long>();
        long sum = 0;
        for(int i = 0; i < nums.length; i++) {
            sum += (long) nums[i];
            valSet.add(sum);
        }

        Long[] valArr = valSet.toArray(new Long[0]);

        Arrays.sort(valArr);
        SegmentTreeNode root = buildSegmentTree(valArr, 0, valArr.length-1);

        for(int i = nums.length-1; i >=0; i--) {
            updateSegmentTree(root, sum);
            sum -= (long) nums[i];
            ans += getCount(root, (long)lower+sum, (long)upper+sum);
        }
        return ans;
    }

}

```

####BST
- [BST](http://www.cnblogs.com/EdwardLiu/p/5138198.html)

```
	Time: O(NlogN)

	这个做法是建立BST，把prefix sum作为TreeNode.val存进去，为了避免重复的TreeNode.val处理麻烦，设置一个count记录多少个重复TreeNode.val, 维护leftSize, 记录比该节点value小的节点个数，rightSize同理

	由于RangeSum S(i,j)在[lower,upper]之间的条件是lower<=sums[j+1]-sums[i]<=upper, 所以我们每次insert一个新的PrefixSum sums[k]进这个BST之前，先寻找一下（rangeSize）该BST内已经有多少个PrefixSum（叫它sums[t]吧）满足lower<=sums[k]-sums[t]<=upper, 即寻找有多少个sums[t]满足：

	sums[k]-upper<=sums[t]<=sums[k]-lower

	BST提供了countSmaller和countLarger的功能，计算比sums[k]-upper小的RangeSum数目和比sums[k]-lower大的数目，再从总数里面减去，就是所求
```

```java
public class Solution {
    private class TreeNode {
        long val = 0;
        int count = 1;
        int leftSize = 0;
        int rightSize = 0;
        TreeNode left = null;
        TreeNode right = null;
        public TreeNode(long v) {
            this.val = v;
            this.count = 1;
            this.leftSize = 0;
            this.rightSize = 0;
        }
    }

    private TreeNode insert(TreeNode root, long val) {
        if(root == null) {
            return new TreeNode(val);
        } else if(root.val == val) {
            root.count++;
        } else if(val < root.val) {
            root.leftSize++;
            root.left = insert(root.left, val);
        } else if(val > root.val) {
            root.rightSize++;
            root.right = insert(root.right, val);
        }
        return root;
    }

    private int countSmaller(TreeNode root, long val) {
        if(root == null) {
            return 0;
        } else if(root.val == val) {
            return root.leftSize;
        } else if(root.val > val) {
            return countSmaller(root.left, val);
        } else {
            return root.leftSize + root.count + countSmaller(root.right, val);
        }
    }

    private int countLarger(TreeNode root, long val) {
        if(root == null) {
            return 0;
        } else if(root.val == val) {
            return root.rightSize;
        } else if(root.val < val) {
            return countLarger(root.right, val);
        } else {
            return countLarger(root.left, val) + root.count + root.rightSize;
        }
    }

    private int rangeSize(TreeNode root, long lower, long upper) {
        int total = root.count + root.leftSize + root.rightSize;
        int smaller = countSmaller(root, lower);    // Exclude everything smaller than lower
        int larger = countLarger(root, upper);      // Exclude everything larger than upper
        return total - smaller - larger;
    }

    public int countRangeSum(int[] nums, int lower, int upper) {
        if(nums.length == 0) {
            return 0;
        }
        long[] sums = new long[nums.length + 1];
        for(int i = 0; i < nums.length; i++) {
            sums[i + 1] = sums[i] + nums[i];
        }
        TreeNode root = new TreeNode(sums[0]);
        int output = 0;
        for(int i = 1; i < sums.length; i++) {
            output += rangeSize(root, sums[i] - upper, sums[i] - lower);
            insert(root, sums[i]);
        }
        return output;
    }
}
```
