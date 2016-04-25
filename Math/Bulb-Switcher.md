##Bulb Switcher

Difficulty: Medium

	There are n bulbs that are initially off.
	You first turn on all the bulbs.
	Then, you turn off every second bulb.
	On the third round, you toggle every third bulb
	(turning on if it's off or turning off if it's on).
	For the ith round, you toggle every i bulb.
	For the nth round, you only toggle the last bulb.
	Find how many bulbs are on after n rounds.

	Example:

	Given n = 3.

	At first, the three bulbs are [off, off, off].
	After first round, the three bulbs are [on, on, on].
	After second round, the three bulbs are [on, off, on].
	After third round, the three bulbs are [on, off, off].

	So you should return 1, because there is only one bulb is on.

####思路
- 暴力

```java
public class Solution {
    public int bulbSwitch(int n) {
        if (n <= 0) {
            return 0;
        }

        boolean[] light = new boolean[n];
        for (int i = 0; i < n; i++) {
            light[i] = false;
        }

        for (int i = 1; i < n; i++) {
            for (int j = 0; j < n; j += i) {
                light[j] = !light[j];
            }
        }

        int count = 0;
        for (int i = 0; i < n; i++) {
            if (light[i]) {
                count++;
            }
        }
        return count;
    }
}

####优化

	对于素数，那么它仅有1和它本身，最后一定是关掉的。

	对一普通的，一定是关掉的，因子成对出现

	对于完全平方数，因为有一个倍数不成对出现，所以一定是打开的。比如4 => 1,4   | 2

	所以本题就是求1~n有几个完全平方数。

	那么，怎么求呢?从1开始到n，每个数测试一下？时间复杂度O(n)，太慢

	正确的是直接sqrt(n)，就可以算出来啦~

```java
public class Solution {
    public int bulbSwitch(int n) {
        if (n <= 0) {
            return 0;
        }

        int result = 1;

        while (result * result <= n) result++;
        return result - 1;
    }
}
```

####再优化
```java
public class Solution {
    public int bulbSwitch(int n) {
        if (n <= 0) {
            return 0;
        }

        return Math.sqrt(n);
    }
}
```
