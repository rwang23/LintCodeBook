##Subarray Sum Closest

16% Accepted

	Given an integer array, find a subarray with sum closest to zero.
    Return the indexes of the first number and last number.

	Have you met this question in a real interview? Yes
	Example
	Given [-3, 1, 1, -3, 5], return [0, 2], [1, 3], [1, 1], [2, 2] or [0, 4].

####Challenge
O(nlogn) time

####Tags Expand
- Subarray Sort

####思路
- 第一种方法：直接遍历,在两重循环里边找 O(n3)
- 第二种方法：设置prefixsum,在两重循环里边找 O(n2)
- 第三种方法：利用prefixsum与treemap的思想（treemap可以把key/val一起存起来，而且根据key的升序排序），把prefixsum/i存进去，然后排序，就得到了按升序排列的prefixsum，而且对应的key也没有丢掉
- The TreeMap class implements the Map interface by using a tree. A TreeMap provides an efficient means of storing key/value pairs in sorted order, and allows rapid retrieval.
- 本题中，没有直接调用treemap,而是写了一个简要的pair,实现了相似的功能。 写了pair后，要自己写Comparator<pairr>去实现排序
- 因为排序后，相邻的prefixsum之差是最小的，所以计算相邻的，再比较每次替换就可以了。不行的话，将已经写入的Arraylist 进行clear操作

```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: A list of integers includes the index of the first number
     *          and the index of the last number
     */
    class Pair {
        int sum;
        int index;
        public Pair(int s, int i) {
            sum = s;
            index = i;
        }
    }
    public ArrayList<Integer> subarraySumClosest(int[] nums) {
        // write your code here
        ArrayList<Integer> res = new ArrayList<Integer> ();
        if (nums == null || nums.length == 0) {
            return res;
        }

        int len = nums.length;
        if(len == 1) {
            res.add(0);
            res.add(0);
            return res;
        }
        Pair[] prefixsum = new Pair[len+1];
        int prev = 0;
        prefixsum[0] = new Pair(0, 0);
        for (int i = 1; i <= len; i++) {
            prefixsum[i] = new Pair(prev + nums[i-1], i);
            prev = prefixsum[i].sum;
        }
        Arrays.sort(prefixsum, new Comparator<Pair>() {
           public int compare(Pair a, Pair b) {
               return a.sum - b.sum;
           }
        });
        int ans = Integer.MAX_VALUE;
        for (int i = 1; i <= len; i++) {

            if (ans > prefixsum[i].sum - prefixsum[i-1].sum) {
                ans = prefixsum[i].sum - prefixsum[i-1].sum;
                res.clear();
                int[] temp = new int[]{prefixsum[i].index - 1, prefixsum[i - 1].index - 1};
                Arrays.sort(temp);
                res.add(temp[0] + 1);
                res.add(temp[1]);
            }
        }

        return res;
    }
}
```
