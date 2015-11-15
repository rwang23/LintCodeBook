####Largest Number

17% Accepted

	Given a list of non negative integers, arrange them such that they form the largest number.

	Have you met this question in a real interview? Yes
	Example
	Given [1, 20, 23, 4, 8], the largest formed number is 8423201.

	Note
	The result may be very large, so you need to return a string instead of an integer.

####Tags Expand
LintCode Copyright Sort


####



####我的解法
- Time O(n2) Space O(n) 比较笨的办法
- 先将所有数利用辅助数组都提升到一个数量级，比如[8,200,41，410] ---> [800,200,411，410] 41不是到410而是411， 这样41比411更有优先级
- 注意如果是[0,0] 只输出"0"，所以如果有多个0只输出一次
- 使用了stringbuffer加速string的效率

```java
public class Solution {
    /**
     *@param num: A list of non negative integers
     *@return: A string
     */
    public String largestNumber(int[] num) {
        // write your code here
        if (num == null || num.length == 0) {
            return null;
        }

        StringBuffer largestNum = new StringBuffer("");
        long max = 0;
        for (int i = 0; i < num.length; i++) {
            max = Math.max(max, num[i]);
        }
        int limit = 1;
        while (max > 10) {
            max = max / 10;
            limit = limit * 10;
        }
        long[] aux = new long[num.length];
        for (int i = 0; i < num.length; i++) {
            aux[i] = (long)num[i];
            long one = aux[i] % 10;
            while (aux[i] < limit && aux[i] != 0) {
                aux[i] = aux[i] * 10 + one ;
            }
        }


        int index = 0;
        boolean trailingZero = false;

        for (int i = 0; i < num.length; i++) {
            max = -1;
            for (int j = 0; j < num.length; j++) {
                if (aux[j] > max) {
                    max = aux[j];
                    index = j;
                }
            }
            aux[index] = -1;
            if (!trailingZero) {
                if (num[index] == 0) {
                    trailingZero = true;
                }
                largestNum.append(num[index]);
            }
        }

        return largestNum.toString();

    }
}

```

####正规解法
- 使用了string的comparator让其自动排序
- string排序就解决了之前我考虑的计算的问题

```java
class NumbersComparator implements Comparator<String> {
	@Override
	public int compare(String s1, String s2) {
		return (s2 + s1).compareTo(s1 + s2);
	}
}

public class Solution {

    public String largestNumber(int[] nums) {
        String[] strs = new String[nums.length];
        for (int i = 0; i < nums.length; i++) {
            strs[i] = Integer.toString(nums[i]);
        }
        Arrays.sort(strs, new NumbersComparator());
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < strs.length; i++) {
            sb.append(strs[i]);
        }
        String result = sb.toString();
        int index = 0;
        while (index < result.length() && result.charAt(index) == '0') {
            index++;
        }
        if (index == result.length()) {
            return "0";
        }
        return result.substring(index);
    }
}
```
