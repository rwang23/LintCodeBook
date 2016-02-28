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
- [参考](http://blog.csdn.net/xudli/article/details/46798619)
- 每10个数, 有一个个位是1, 每100个数, 有10个十位是1, 每1000个数, 有100个百位是1.  做一个循环, 每次计算单个位上1得总个数(个位,十位, 百位).

#
    以算百位上1为例子:   假设百位上是0, 1, 和 >=2 三种情况:
        case 1: n=3141092, a= 31410, b=92. 计算百位上1的个数应该为 3141 *100 次.
        case 2: n=3141192, a= 31411, b=92. 计算百位上1的个数应该为 3141 *100 + (92+1) 次.
        case 3: n=3141592, a= 31415, b=92. 计算百位上1的个数应该为 (3141+1) *100 次.
    以上三种情况可以用 一个公式概括:

    十位数上的数字(加1)就代表1出现的个数，这时候我们再把多出的10个加上即可。比如56就有(5+1)+10=16个。如何知道是否要加上多出的10个呢，我们就要看十位上的数字是否大于等于2，是的话就要加上多余的10个'1'。那么我们就可以用(x+8)/10来判断一个数是否大于等于2
    (a + 8) / 10 * m + (a % 10 == 1) * (b + 1);

```java
public class Solution {
    public int countDigitOne(int n) {
        int ones = 0;
        for (long m = 1; m <= n; m *= 10) {
            long a = n/m, b = n%m;
            ones += (a + 8) / 10 * m;
            if(a % 10 == 1) ones += b + 1;
        }
        return ones;
    }
}
```

####另一种更好理解的递归解法
- (参考)[http://yuanhsh.iteye.com/blog/2227478]

#
    Solution:
    For example '8192':

    1-999 -> countDigitOne(999)

    1000-1999 -> 1000 of 1s + countDigitOne(999)

    2000-2999 -> countDigitOne(999)

    .

    .

    7000-7999 -> countDigitOne(999)

    8000-8192 -> countDigitOne(192)

    Count of 1s : countDigitOne(999)*8 + 1000 + countDigitOne(192)

    Noticed that, if the target is '1192':

    Count of 1s : countDigitOne(999)*1 + (1192 - 1000 + 1) + countDigitOne(192)

    (1192 - 1000 + 1) is the 1s in thousands from 1000 to 1192.

```java
public int countDigitOne(int n) {

    if(n <= 0) return 0;
    if(n < 10) return 1;

    int base = (int)Math.pow(10, (n + "").length() - 1);
    int k = n / base;

    return countDigitOne(base - 1) * k +
            (k == 1 ? (n- base + 1) : base) +
            countDigitOne(n % base);
}
```
