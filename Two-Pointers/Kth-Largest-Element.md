##Kth Largest Element

19% Accepted

	Find K-th largest element in an array.

	Have you met this question in a real interview? Yes
	Example
	In array [9,3,2,4,8], the 3rd largest element is 4.

	In array [1,2,3,4,5], the 1st largest element is 5, 2nd largest element is 4, 3rd largest element is 3 and etc.

	Note
	You can swap elements in the array

####Challenge
- O(n) time, O(1) extra memory.

####Tags Expand
- Quick Sort
- Sort


####思路
- quick select

```java
class Solution {
    //param k : description of k
    //param numbers : array of numbers
    //return: description of return
    public int kthLargestElement(int k, ArrayList<Integer> numbers) {
        // write your code here
        int lo = 0;
        int hi = numbers.size() - 1;
        k = numbers.size() - k;
        while (lo < hi) {
            int j = partition(numbers, lo, hi);
            if (k > j) {
                lo = j + 1;
            } else if (k < j) {
                hi = j - 1;
            } else {
                return numbers.get(k).intValue();
            }
        }
        return numbers.get(k).intValue();

    }

    public int partition(ArrayList<Integer> numbers, int lo, int hi) {
        int start = lo;
        int end = hi + 1;
        while (start < end) {
            while (numbers.get(++start) < numbers.get(lo)) {
                if (start == hi) {
                    break;
                }
            }
            while (numbers.get(--end) > numbers.get(lo)) {
                if (end == lo) {
                    break;
                }
            }
            if (start >= end) {
                break;
            }
            swap(numbers, start, end);
        }
        swap(numbers, lo, end);
        return end;
    }

    public void swap(ArrayList<Integer> numbers, int lo, int hi) {
        int temp = numbers.get(lo).intValue();
        numbers.set(lo, numbers.get(hi).intValue());
        numbers.set(hi, temp);
    }

};

```
