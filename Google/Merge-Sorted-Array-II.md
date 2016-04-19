##Merge Sorted Array II

	Merge two given sorted integer array A and B into a new sorted integer array.

	Have you met this question in a real interview? Yes
	Example
	A=[1,2,3,4]

	B=[2,4,5,6]

	return [1,2,2,3,4,4,5,6]

####Challenge
How can you optimize your algorithm if one array is very large and the other is very small?

####Tags Expand
Sorted Array Array


####常规解法
- 这个解法用了o(n) space

```java
class Solution {
    /**
     * @param A and B: sorted integer array A and B.
     * @return: A new sorted integer array
     */
    public ArrayList<Integer> mergeSortedArray(ArrayList<Integer> A, ArrayList<Integer> B) {
        // write your code here
        int m = A.size();
        int n = B.size();
        ArrayList<Integer> aux = new ArrayList<Integer>();
        int i = 0;
        int j = 0;
        while(i!=m || j!=n){
            if(i == m){
                aux.add(B.get(j).intValue());
                j++;
            } else if(j == n){
                aux.add(A.get(i).intValue());
                i++;
            } else if(A.get(i).intValue()>=B.get(j).intValue()){
                aux.add(B.get(j).intValue());
                j++;
            } else{
                aux.add(A.get(i).intValue());
                i++;
            }
        }
        return aux;

    }
}

```

####九章解法
- 这个解法没有占用空间,但是速度比较慢,因为人家已经排好序了
- o(nlogn)

```java
class Solution {
    /**
     * @param A and B: sorted integer array A and B.
     * @return: A new sorted integer array
     */
    public ArrayList<Integer> mergeSortedArray(ArrayList<Integer> A, ArrayList<Integer> B) {
        int len = B.size();
        for (int i = 0; i < len; ++i)
            A.add(B.get(i));
        Collections.sort(A);
        return A;
    }
}
```

####如果是数组的话,最好解法
- O(n) 不消耗空间

```java
class Solution {
    /**
     * @param A: sorted integer array A which has m elements,
     *           but size of A is m+n
     * @param B: sorted integer array B which has n elements
     * @return: void
     */
    public void mergeSortedArray(int A[], int m, int B[], int n) {
        int index = n + m;

        while (m > 0 && n > 0) {
            if (A[m - 1] > B[n - 1]) {
                A[--index] = A[--m];
            } else {
                A[--index] = B[--n];
            }
        }
        while (n > 0) {
            A[--index] = B[--n];
        }
        while (m > 0) {
            A[--index] = A[--m];
        }
    }
};
```
