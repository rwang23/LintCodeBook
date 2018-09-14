##3 Sum

19% Accepted

	Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0?
    Find all unique triplets in the array which gives the sum of zero.

	Have you met this question in a real interview? Yes
	Example
	For example, given array S = {-1 0 1 2 -1 -4}, A solution set is:

	(-1, 0, 1)
	(-1, -1, 2)
	Note
	Elements in a triplet (a,b,c) must be in non-descending order. (ie, a ≤ b ≤ c)

	The solution set must not contain duplicate triplets.

####Tags Expand
- Two Pointers
- Sort Array

####思路
- Two Sum变形，多了一个循环
- 这个List里边的contains,检查Integer,String,List<Integer>这种的时候,是比较的value,而不是地址
- list1.equals(list2)
	From the javadoc:

	Compares the specified object with this list for equality. Returns true if and only if the specified object is also a list, both lists have the same size, and all corresponding pairs of elements in the two lists are equal.

```java
public class Solution {
    /**
     * @param numbers : Give an array numbers of n integer
     * @return : Find all unique triplets in the array which gives the sum of zero.
     */
    public ArrayList<ArrayList<Integer>> threeSum(int[] numbers) {
        // write your code here
        if (numbers == null || numbers.length < 3 ) {
            return null;
        }
        Arrays.sort(numbers);
        ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>>();
        for (int i = 0; i < numbers.length - 2; i++) {
            if (i != 0 && numbers[i] == numbers[i - 1]) {
				continue; // to skip duplicate numbers; e.g [0,0,0,0]
			}
            int target =  0 - numbers[i];
            int start = i + 1;
            int end = numbers.length - 1;
            while (start < end) {
                ArrayList set = new ArrayList();

                if (numbers[start] + numbers[end] > target) {
                    end--;
                } else if (numbers[start] + numbers[end] < target) {
                    start++;
                } else {
                    set.add(numbers[i]);
                    set.add(numbers[start]);
                    set.add(numbers[end]);

                    if(!res.contains(set)){
                        res.add(set);
                    }
                    start++;
                    end--;
                    while (start < end && numbers[start] == numbers[start - 1]){
                        start++;
                    }
                    while (start < end && numbers[end] == numbers[end + 1]) {
                        end--;
                    }
                }
            }
        }
        return res;
    }
}

```

####后来写的,容易理解一点
- 还有一个点是,要去重,不然重复的太多了
- Input里边可能有很多duplicate,有的过了直接skip就行,省去了大量时间

```java
public class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if (nums == null || nums.length <= 2) {
            return result;
        }
        Arrays.sort(nums);
        int len = nums.length;
        for (int i = 0; i < len; i++) {
            if (i != 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int target = 0 - nums[i];
            int start = i + 1;
            int end = len - 1;
            while (start < end) {
                int sum = nums[start] + nums[end];
                if (sum == target) {
                    //List<Integer> list = new ArrayList<Integer>();
                    result.add(Arrays.asList(nums[i], nums[start], nums[end]));
                    start++;
                    end--;
                    while (start < end && nums[start] == nums[start - 1]){
                        start++;
                    }
                    while (start < end && nums[end] == nums[end + 1]) {
                        end--;
                    }
                } else if (sum > target) {
                    end--;
                } else {
                    start++;
                }
            }
        }
        return result;
    }
}
```
