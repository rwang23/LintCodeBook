##Sqrt(x)

23% Accepted

	Implement int sqrt(int x).

	Compute and return the square root of x.

	Have you met this question in a real interview? Yes
	Example
	sqrt(3) = 1

	sqrt(4) = 2

	sqrt(5) = 2

	sqrt(10) = 3

####Challenge
O(log(x))

####Tags Expand
Binary Search Mathematics

```java
class Solution {
    /**
     * @param x: An integer
     * @return: The sqrt of x
     */
    public int sqrt(int x) {
        // write your code here
        if(x==1){
            return 1;
        }
        if(x<=0){
            return 0;
        }
        int hi = x;
        int lo = 0;
        int mid = (lo+hi)/2;
        while(lo<=hi){

            if((long)mid*mid>(long)x){
                hi = mid-1;
                mid = (lo+hi)/2;
            }else if((long)mid*mid<(long)x){
                lo = mid+1;
                mid = (lo+hi)/2;
            }else{
                return mid;
            }

        }
        return mid;
    }
}
```
