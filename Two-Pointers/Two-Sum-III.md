##Two Sum III - Data structure design
  Design and implement a TwoSum class. It should support the following operations: add and find.

  add - Add the number to an internal data structure.
  find - Find if there exists any pair of numbers which sum is equal to the value.

###Example
    add(1); add(3); add(5);
    find(4) // return true
    find(7) // return false

###思路
 - 这道题有很多种解法，取决于到底是add使用的多还是find使用的多
 - 如果是find使用的多，那么就用set，每次在add的时候算出来sum存进去
 - 如果是add多，那么就两根指针

```
 解法:
 linkedlist add O(n) find O(n)

 list add O(1) find O(nlogn)

 treemap add O(logn) find O(n)

 map + list add O(1) find O(n)
```

```java
//map + list 使用减法来找是否存在另一个数满足和
 public class TwoSum {

    private List<Integer> list = null;
    private Map<Integer, Integer> map = null;
    public TwoSum() {
        list = new ArrayList<Integer>();
        map = new HashMap<Integer, Integer>();
    }

    // Add the number to an internal data structure.
    public void add(int number) {
        // Write your code here
        if (map.containsKey(number)) {
            map.put(number, map.get(number) + 1);
        } else {
            map.put(number, 1);
            list.add(number);
        }
    }

    // Find if there exists any pair of numbers which sum is equal to the value.
    public boolean find(int value) {
        // Write your code here
        for (int i = 0; i < list.size(); i++) {
            int num1 = list.get(i), num2 = value - num1;
            if ((num1 == num2 && map.get(num1) > 1) ||
                (num1 != num2 && map.containsKey(num2)))
                return true;
        }
        return false;
    }
}

```

```java
 //list
 public class TwoSum {
    /**
     * @param number: An integer
     * @return: nothing
     */
    List<Integer> list = new ArrayList<Integer>();
    public void add(int number) {
        // write your code here
        list.add(number);

    }

    /**
     * @param value: An integer
     * @return: Find if there exists any pair of numbers which sum is equal to the value.
     */
    public boolean find(int value) {
        // write your code here
        Collections.sort(list);

        int start = 0;
        int end = list.size() - 1;

        while (start < end) {
            int startValue = list.get(start);
            int endValue = list.get(end);

            if (startValue + endValue > value) {
                end--;
            } else if (startValue + endValue < value) {
                start++;
            } else {
                return true;
            }
        }

        return false;
    }

```
