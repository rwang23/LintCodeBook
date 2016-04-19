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

####O(n2) 做法
- 测试结果与 答案一模一样,就是在Lintcode上未能通过 不知原因
- 尾部还添加了ArrayList<ArrayList<Integer>> 排序的comparator

```java
public class Solution {
    /**
     * @param numbers : Give an array numbersbers of n integer
     * @param target : you need to find four elements that's sum of target
     * @return : Find all unique quadruplets in the array which gives the sum of
     *           zero.
     */
    private class Pair {
        Integer x;
        Integer y;
        Pair(int x, int y) {
            this.x = x;
            this.y = y;
        }

        // @Override
        // public int hashCode(){
        //     return this.x.hashCode() + this.y.hashCode();
        // }

        // @Override
        // public boolean equals(Object d) {
        //     if (!(d instanceof Pair)) {
        //         return false;
        //     }
        //     Pair p = (Pair)d;
        //     return (this.x == p.x) && (this.y == p.y);
        // }
    }

    public ArrayList<ArrayList<Integer>> fourSum(int[] numbers, int target) {
        /* your code */
        if (numbers == null || numbers.length < 3) {
            return new ArrayList<ArrayList<Integer>>();
        }
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
        HashMap<Pair, Integer> map = new HashMap<Pair, Integer>();
        int size = numbers.length;
        Arrays.sort(numbers);
        for (int i = 1; i < size; i++) {
            for (int j = 0; j < i; j++) {
                Pair pair = new Pair(i, j);
                map.put(pair, numbers[i] + numbers[j]);
            }
        }

        for (Map.Entry<Pair, Integer> entry : map.entrySet()) {
            Pair pair = entry.getKey();
            int sum = entry.getValue();
            int index1 = pair.x;
            int index2 = pair.y;
            int newTarget = target - sum;
            int start = 0;
            int end = size - 1;
            while (start < end) {
                ArrayList<Integer> list = new ArrayList<Integer>();
                if (start == index1 || start == index2) {
                    start++;
                    continue;
                }
                if (end == index1 || end == index2) {
                    end--;
                    continue;
                }

                if (numbers[start] + numbers[end] > newTarget) {
                    end--;
                } else if (numbers[start] + numbers[end] < newTarget) {
                    start++;
                } else {
                    list.add(numbers[index1]);
                    list.add(numbers[index2]);
                    list.add(numbers[start]);
                    list.add(numbers[end]);
                    Collections.sort(list);
                    if (!result.contains(list)) {
                        result.add(list);
                    }
                    start++;
                    end--;
                }
            }
        }
        Collections.sort(result, new Comparator<ArrayList<Integer>>() {
            public int compare(ArrayList<Integer> o1, ArrayList<Integer> o2) {
                int size = o1.size() > o2.size() ? o2.size() : o1.size();
                for (int i = 0; i < size; i++) {
                    if (o1.get(i) != o2.get(i)) {
                        return o1.get(i).compareTo(o2.get(i));
                    } else {
                        continue;
                    }
                }
                return o1.get(0).compareTo(o2.get(0));
            }
        });
        return result;
    }
}
```

####eclipse测试 与 答案一模一样,就是在Lintcode上未能通过 不知原因
```java
import java.security.KeyStore.Entry;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.HashMap;
import java.util.Map;


public class Solution {
    /**
     * @param str a string
     * @return all permutations
     */
    static class Pair {
        Integer x;
        Integer y;
        public Pair(int x, int y) {
            this.x = x;
            this.y = y;
        }

        // @Override
        // public int hashCode(){
        //     return this.x.hashCode() + this.y.hashCode();
        // }

        // @Override
        // public boolean equals(Object d) {
        //     if (!(d instanceof Pair)) {
        //         return false;
        //     }
        //     Pair p = (Pair)d;
        //     return (this.x == p.x) && (this.y == p.y);
        // }
    }

    public static ArrayList<ArrayList<Integer>> fourSum(int[] numbers, int target) {
        /* your code */
        if (numbers == null || numbers.length < 3) {
            return new ArrayList<ArrayList<Integer>>();
        }
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
        HashMap<Pair, Integer> map = new HashMap<Pair, Integer>();
        int size = numbers.length;
        Arrays.sort(numbers);
        for (int i = 1; i < size; i++) {
            for (int j = 0; j < i; j++) {
                Pair pair = new Pair(i, j);
                map.put(pair, numbers[i] + numbers[j]);
            }
        }

        for (Map.Entry<Pair, Integer> entry : map.entrySet()) {
            Pair pair = entry.getKey();
            int sum = entry.getValue();
            int index1 = pair.x;
            int index2 = pair.y;
            int newTarget = target - sum;
            int start = 0;
            int end = size - 1;
            while (start < end) {
                ArrayList<Integer> list = new ArrayList<Integer>();
                if (start == index1 || start == index2) {
                    start++;
                    continue;
                }
                if (end == index1 || end == index2) {
                    end--;
                    continue;
                }

                if (numbers[start] + numbers[end] > newTarget) {
                    end--;
                } else if (numbers[start] + numbers[end] < newTarget) {
                    start++;
                } else {
                    list.add(numbers[index1]);
                    list.add(numbers[index2]);
                    list.add(numbers[start]);
                    list.add(numbers[end]);
                    Collections.sort(list);
                    if (!result.contains(list)) {
                        result.add(list);
                    }
                    start++;
                    end--;
                }
            }
        }
        Collections.sort(result, new Comparator<ArrayList<Integer>>() {
            public int compare(ArrayList<Integer> o1, ArrayList<Integer> o2) {
                int size = o1.size() > o2.size() ? o2.size() : o1.size();
                for (int i = 0; i < size; i++) {
                    if (o1.get(i) != o2.get(i)) {
                        return o1.get(i).compareTo(o2.get(i));
                    } else {
                        continue;
                    }
                }
                return o1.get(0).compareTo(o2.get(0));
            }
        });
        return result;
    }

    public static void main(String[] input) {
        int[] nums = new int[]{0,0,-1012,0,0,0,-3002,0,0,0,-10,-19,0,0,90,0,92,0,1,1,1,9,9,9,10,11,1001,2001,-404,201,203,201,999,345,1,1,1,1,1,1,1,-2,1,1,1,1,1,-1,1,1,-2,1,1,1,1,3,1,1,1,1,1,-1200,1,1,1,1,1,2,1202,2,2,-4,2,2,2,2,4,5,6,1,1,-11,1,1,1,1,1,1,1,1,101,1,1,1,1,1,-1,1,-6};
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
        result = fourSum(nums, 92);
        for (int i = 0; i < result.size(); i++) {
            ArrayList<Integer> list = result.get(i);
            for (int j = 0; j < list.size(); j++) {
                int cur = list.get(j);
                System.out.print(cur);
                System.out.print(", ");
            }
            System.out.println("");
        }
    }
}
```
####测试结果 与 答案一模一样,就是在Lintcode上未能通过 不知原因
    [[-3002,92,1001,2001],
    [-1200,-11,101,1202],
    [-1200,-2,92,1202],
    [-1200,0,90,1202],
    [-1200,90,201,1001],
    [-1200,90,203,999],
    [-1200,92,201,999],
    [-1012,2,101,1001],
    [-1012,4,101,999],
    [-1012,11,92,1001],
    [-404,92,201,203],
    [-19,-1,11,101],
    [-19,0,10,101],
    [-19,1,9,101],
    [-19,4,6,101],
    [-19,9,10,92],
    [-19,10,11,90],
    [-11,-4,6,101],
    [-11,-2,4,101],
    [-11,-1,3,101],
    [-11,0,2,101],
    [-11,0,11,92],
    [-11,1,1,101],
    [-11,1,10,92],
    [-11,2,9,92],
    [-11,2,11,90],
    [-11,3,10,90],
    [-11,4,9,90],
    [-11,5,6,92],
    [-10,-4,5,101],
    [-10,-2,3,101],
    [-10,-1,2,101],
    [-10,-1,11,92],
    [-10,0,1,101],
    [-10,0,10,92],
    [-10,1,9,92],
    [-10,1,11,90],
    [-10,2,10,90],
    [-10,3,9,90],
    [-10,4,6,92],
    [-6,-4,1,101],
    [-6,-4,10,92],
    [-6,-2,-1,101],
    [-6,-2,10,90],
    [-6,-1,9,90],
    [-6,0,6,92],
    [-6,1,5,92],
    [-6,2,4,92],
    [-6,2,6,90],
    [-6,3,5,90],
    [-4,-2,6,92],
    [-4,-1,5,92],
    [-4,0,4,92],
    [-4,0,6,90],
    [-4,1,3,92],
    [-4,1,5,90],
    [-4,2,2,92],
    [-4,2,4,90],
    [-2,-2,4,92],
    [-2,-2,6,90],
    [-2,-1,3,92],
    [-2,-1,5,90],
    [-2,0,2,92],
    [-2,0,4,90],
    [-2,1,1,92],
    [-2,1,3,90],
    [-2,2,2,90],
    [-1,-1,2,92],
    [-1,-1,4,90],
    [-1,0,1,92],
    [-1,0,3,90],
    [-1,1,2,90],
    [0,0,0,92],
    [0,0,2,90],
    [0,1,1,90]]
