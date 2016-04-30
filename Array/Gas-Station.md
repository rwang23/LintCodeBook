##Gas Station

	Total Accepted: 60288 Total Submissions: 220483 Difficulty: Medium
	There are N gas stations along a circular route, where the amount of gas at station i is gas[i].

	You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

	Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.

####思路
- brute force, 从每个节点开始算为起始点,O(n2)

```java
public class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        if (gas.length != cost.length) {
            return -1;
        }

        int len = gas.length;

        for (int i = 0; i < len; i++) {
            int startGas = 0;
            for (int start = i; start < i + len; start++) {
                int index = start;
                if (start >= len) {
                    index = start - len;
                }
                startGas += gas[index];
                startGas -= cost[index];
                if (startGas < 0) {
                    break;
                }
                if (start == i + len - 1) {
                    return index;
                }
            }
        }

        return -1;
    }
}
```

####两个指针思想
- 利用两个指针思想
- 不用通过每个节点再去找
- 找一个,如果不行,就把这个作为起始点,
- 所以用时也就是O(2n) 也就是O(n)


```java
public class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        if (gas.length != cost.length) {
            return -1;
        }

        int len = gas.length;

        int start = 0;
        int end = len - 1;
        int sum = 0;
        int index = 0;
        while (start <= end && end <= 2* len - 1 ) {
            int curIndex = start;
            if (start >= len) {
                curIndex = start - len;
            }

            sum += gas[curIndex];
            sum -= cost[curIndex];

            if (sum < 0) {
                start = start + 1;
                index = start;
                sum = 0;
                end = len - 1 + start;
            } else {
                if (start - index == len - 1) {
                    return index;
                }
                start++;
            }
        }

        return -1;
    }
}
```
