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
```java
public class Solution {
    /**
     * @param numbers : Give an array numbers of n integer
     * @return : Find all unique triplets in the array which gives the sum of zero.
     */
    public ArrayList<ArrayList<Integer>> threeSum(int[] numbers) {
        // write your code here
        if (numbers == null || numbers.length <= 2) {
            return new ArrayList<ArrayList<Integer>>();
        }
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
        int size = numbers.length;
        Arrays.sort(numbers);

        for (int i = 0; i < size; i++) {
            int target = 0 - numbers[i];
            int start = i + 1;
            int end = size - 1;
            while (start <  end) {
                ArrayList<Integer> list = new ArrayList<Integer>();
                if (numbers[start] + numbers[end] > target) {
                    end--;
                } else if (numbers[start] + numbers[end] < target) {
                    start++;
                } else {
                    list.add(numbers[i]);
                    list.add(numbers[start]);
                    list.add(numbers[end]);
                    if (!result.contains(list)) {
                        result.add(list);
                    }
                    start++;
                }
            }
        }
        return result;

    }
}
```
