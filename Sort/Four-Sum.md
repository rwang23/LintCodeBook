##4 Sum

19% Accepted

	Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target?
    Find all unique quadruplets in the array which gives the sum of target.

	Have you met this question in a real interview? Yes
	Example
	For example, given array S = {1 0 -1 0 -2 2}, and target = 0. A solution set is:

	(-1, 0, 0, 1)

	(-2, -1, 1, 2)

	(-2, 0, 0, 2)

	Note
	Elements in a quadruplet (a,b,c,d) must be in non-descending order. (ie, a ≤ b ≤ c ≤ d)

	The solution set must not contain duplicate quadruplets.

####Tags Expand
- Two Pointers
- Sort
- Hash Table
- Array

####思路
- O(n3)的话，就按照3 sum的思路就行
- 也有使用hashmap把一对数的和存起来的，变成two sum,时间复杂度变成O(n2) 最坏情况的是o(n3)

####O(n3)
```java
public class Solution {
    /**
     * @param numbers : Give an array numbersbers of n integer
     * @param target : you need to find four elements that's sum of target
     * @return : Find all unique quadruplets in the array which gives the sum of
     *           zero.
     */
    public ArrayList<ArrayList<Integer>> fourSum(int[] numbers, int target) {
        ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>>();
        if (numbers == null || numbers.length < 3 ) {
            return res;
        }
        Arrays.sort(numbers);
        for (int i = 0; i < numbers.length - 3; i++) {
            if (i != 0 && numbers[i] == numbers[i - 1]) {
				continue;
			}
			for (int j = i + 1; j < numbers.length - 2; j++) {
			 //   if (j != 1 && numbers[j] == numbers[j - 1]) {
				//     continue;
			 //   }
			    int find =  target - numbers[i] - numbers[j];
                int start = j + 1;
                int end = numbers.length - 1;
                while (start < end) {
                    ArrayList set = new ArrayList();

                    if (numbers[start] + numbers[end] > find) {
                        end--;
                    } else if (numbers[start] + numbers[end] < find) {
                        start++;
                    } else {
                        set.add(numbers[i]);
                        set.add(numbers[j]);
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
        }
        return res;
    }
}


```
