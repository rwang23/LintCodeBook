##Different Ways to Add Parentheses
	Total Accepted: 17823 Total Submissions: 53485 Difficulty: Medium
	Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. The valid operators are +, - and *.


	Example 1
	Input: "2-1-1".

	((2-1)-1) = 0
	(2-(1-1)) = 2
	Output: [0, 2]


	Example 2
	Input: "2*3-4*5"

	(2*(3-(4*5))) = -34
	((2*3)-(4*5)) = -14
	((2*(3-4))*5) = -10
	(2*((3-4)*5)) = -10
	(((2*3)-4)*5) = 10
	Output: [-34, -14, -10, -10, 10]

####思路
- 见代码
- 思路很明显,就是分治法递归
- 找到左边部分的各种组合,跟右边部分的组合再合并
- 还可以通过hashmap来储存来进行memorization来优化速度

```java
public class Solution {
    public List<Integer> diffWaysToCompute(String input) {
        List<Integer> res = new ArrayList<Integer>();
        for (int i = 0; i < input.length(); i++) {
            char c = input.charAt(i);
            if (c == '-' || c == '+' || c == '*') {
                String a = input.substring(0, i);
                String b = input.substring(i + 1);
                List<Integer> al = diffWaysToCompute(a);
                List<Integer> bl = diffWaysToCompute(b);
                for (int x : al) {
                    for (int y : bl) {
                        if (c == '-') {
                            res.add(x - y);
                        } else if (c == '+') {
                            res.add(x + y);
                        } else if (c == '*') {
                            res.add(x * y);
                        }
                    }
                }
            }
        }
        if (res.size() == 0) res.add(Integer.valueOf(input));
        return res;
    }
}
```
