##Fibonacci

####My first lintcode problem

31% Accepted

	Find the Nth number in Fibonacci sequence.

	A Fibonacci sequence is defined as follow:

	The first two numbers are 0 and 1.
	The i th number is the sum of i-1 th number and i-2 th number.
	The first ten numbers in Fibonacci sequence is:

	0, 1, 1, 2, 3, 5, 8, 13, 21, 34 ...

	Have you met this question in a real interview? Yes
	Example
	Given 1, return 0

	Given 2, return 1

	Given 10, return 34

	Note
	The Nth fibonacci number won't exceed the max value of signed 32-bit integer in the test cases.

####Tags Expand
Enumeration Mathematics Non Recursion


```java
class Solution {
    /**
     * @param n: an integer
     * @return an integer f(n)
     */
    public int fibonacci(int n) {
        // write your code here
        if(n==0){
            return 0;
        }
        ArrayList<Integer> tempArray = new ArrayList<Integer>();
        tempArray.add(0);
        tempArray.add(1);

        for(int i = 2; i<n; i++){
            int sum = tempArray.get(i-2).intValue()+tempArray.get(i-1).intValue();
            tempArray.add(sum);
        }

        return tempArray.get(n-1).intValue();
    }

    // 以下的方法空间复杂度就不想自己写的O(n),他是O(1)
    // public int fibonacci(int n) {
    //         // write your code here
    //         int first = 0;
    //         if(n == 1)
    //             return first;
    //         int second = 1;
    //         if(n == 2)
    //             return second;
    //         int third = 0;
    //         for(int i = 3; i <=n; i++) {
    //             third = first+ second;
    //             first = second;
    //             second = third;
    //         }
    //         return third;
    //     }
}



```
