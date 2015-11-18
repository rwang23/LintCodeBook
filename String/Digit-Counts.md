##Digit Counts

33% Accepted

	Count the number of k's between 0 and n. k can be 0 - 9.

	Have you met this question in a real interview? Yes
	Example
	if n=12, k=1 in [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12], we have FIVE 1's (1, 10, 11, 12)

####Tags Expand
Enumeration


####思路
- 转化成string来做
- integer转化为string strings[i] = Integer.toString(i);
- integer转化为char(只限于0-9) char key = (char) ('0' + k);

```java
class Solution {
    /*
     * param k : As description.
     * param n : As description.
     * return: An integer denote the count of digit k in 1..n
     */
    public int digitCounts(int k, int n) {
        // write your code here
        String[] strings = new String[n+1];
        int count = 0;
        char key = (char) ('0' + k);
        for (int i = 0; i <= n; i++) {
            strings[i] = Integer.toString(i);
            int j = 0;
            String cur = strings[i];
            while (j < cur.length()) {
                if (cur.charAt(j) == key) {
                    count++;
                }
                j++;
            }
        }

        return count;


    }
};


```

####更优的解法
- [参考](http://www.hawstein.com/posts/20.4.html)
