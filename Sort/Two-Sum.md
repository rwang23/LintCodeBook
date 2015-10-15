##2 Sum

27% Accepted

	Given an array of integers, find two numbers such that they add up to a specific target number.

	The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are NOT zero-based.

	Have you met this question in a real interview? Yes
	Example
	numbers=[2, 7, 11, 15], target=9

	return [1, 2]

	Note
	You may assume that each input would have exactly one solution

####Challenge
Either of the following solutions are acceptable:
- O(n) Space, O(nlogn) Time
- O(n) Space, O(n) Time

####Tags Expand
- Two Pointers
- Sort Array


####解法一：排序后使用两根指针

但是排序使用Time O(nlogn), Space O(n)，因为排序后索引掉了，所以必须找索引

```java
public class Solution {
    /*
     * @param numbers : An array of Integer
     * @param target : target = numbers[index1] + numbers[index2]
     * @return : [index1 + 1, index2 + 1] (index1 < index2)
     */
    public int[] twoSum(int[] numbers, int target) {
        // write your code here
        int[] aux = new int[numbers.length];
        for (int k = 0; k < numbers.length; k++) {
            aux[k] = numbers[k];
        }
        Arrays.sort(aux);

        int i = 0;
        int j = numbers.length - 1;
        int[] res = new int[2];
        int temp1 = 0, temp2 = 0;
        while (i < j) {
            if (aux[i] + aux[j] == target) {
                temp1 = aux[i];
                temp2 = aux[j];
                break;
            }
            else if (aux[i] + aux[j] > target) {
                j--;
            }
            else {
                i++;
            }
        }

        boolean flag1 = true, flag2 = true;
        for( int k = 0; k < numbers.length; k++) {
            if (temp1 == numbers[k] && flag1) {
                temp1 = k;
                flag1 = false;
            }
            if (temp2 == numbers[k] && flag2) {
                temp2 = k;
                flag2 = false;
            }
        }
        res[0] = Math.min(temp1, temp2) + 1;
        res[1] = Math.max(temp1, temp2) + 1;
        return res;
    }
}

```
####HashMap
Time O(n) Space O(n)

```java
public class Solution {
    /*
     * @param numbers : An array of Integer
     * @param target : target = numbers[index1] + numbers[index2]
     * @return : [index1 + 1, index2 + 1] (index1 < index2)
     */
     //Using HashMap
    public int[] twoSum(int[] numbers, int target) {
        if (numbers == null || numbers.length == 0) {
            return null;
        }
        int[] rst = new int[2];
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();

        for (int i = 0; i < numbers.length; i++) {
            if (map.containsKey(target - numbers[i])) {
                rst[0] = map.get(target - numbers[i]) + 1;
                rst[1] = i + 1;
            } else {
                map.put(numbers[i], i);
            }
        }
        return rst;
    }
}
```




