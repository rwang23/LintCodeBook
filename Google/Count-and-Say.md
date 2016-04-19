##Count and Say

	Total Accepted: 77246 Total Submissions: 269191 Difficulty: Easy
	The count-and-say sequence is the sequence of integers beginning as follows:
	1, 11, 21, 1211, 111221, ...

	1 is read off as "one 1" or 11.
	11 is read off as "two 1s" or 21.
	21 is read off as "one 2, then one 1" or 1211.
	Given an integer n, generate the nth sequence.

	Note: The sequence of integers will be represented as a string.

####思路
- 简单题硬做

```java
public class Solution {
    public String countAndSay(int n) {
        StringBuilder string = new StringBuilder();
        string.append(1);
        while(n > 1) {
            StringBuilder newS = new StringBuilder();
            int size = string.length();
            char last = string.charAt(0);
            int count = 0;
            for (int i = 0; i < size; i++) {
                char cur = string.charAt(i);
                if (last == cur) {
                    count++;
                } else {
                    newS.append(count);
                    newS.append(last);
                    count = 1;
                    last = cur;
                }

                if (i == size - 1) {
                    newS.append(count);
                    newS.append(cur);
                }
            }
            string = newS;
            n--;
        }
        return string.toString();
    }
}
```
