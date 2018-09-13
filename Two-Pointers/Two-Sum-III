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
 
 ```java
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
}
 ```
