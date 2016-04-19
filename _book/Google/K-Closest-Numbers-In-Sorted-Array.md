##K Closest Numbers In Sorted Array

	Given a target number, a non-negative integer k and an integer array A sorted in ascending order,
	find the k closest numbers to target in A, sorted in ascending order by the difference between the number and target.
	Otherwise, sorted in ascending order by number if the difference is same.

	Example
	Given A = [1, 2, 3], target = 2 and k = 3, return [2, 1, 3].

	Given A = [1, 4, 6, 8], target = 3 and k = 3, return [4, 1, 6].

####Challenge
O(logn + k) time complexity.

####Tags Expand
Binary Search Two Pointers


####最先想到的思路
- 自己建立一个Element类,对value已经difference进行两次排序即可 O(nlogn)
- 后边比较长的数组的时候超时了

```java
public class Solution {
    /**
     * @param A an integer array
     * @param target an integer
     * @param k a non-negative integer
     * @return an integer array
     */
    class Element {
        private int value;
        private int difference;
        Element(int value, int difference) {
            this.value = value;
            this.difference = difference;
        }

    }

    public int[] kClosestNumbers(int[] A, int target, int k) {
        // Write your code here
        if (A == null || A.length < k || k <= 0) {
            return new int[0];
        }

        ArrayList<Element> list = new ArrayList<Element>();
        int[] result = new int[k];
        for (int i = 0; i < A.length; i++) {
            int difference = Math.abs(A[i] - target);
            Element element = new Element(A[i], difference);
            list.add(element);
        }

        Collections.sort(list, new Comparator<Element>(){
            public int compare(Element e1, Element e2) {
                if (e1.difference == e2.difference) {
                    return e1.value - e2.value;
                } else {
                    return e1.difference - e2.difference;
                }
            }
        });

        for (int i = 0; i < k; i++) {
            result[i] = list.get(i).value;
        }

        return result;
    }
}
```

####优化解法
- 先通过二分法找到最接近的点
- 再通过最接近的点找左右k个加入,这个时候用了两根指针
- 注意最近的左右不能超过[0, A.length]的这个范围

```java
public class Solution {
    /**
     * @param A an integer array
     * @param target an integer
     * @param k a non-negative integer
     * @return an integer array
     */

    public int[] kClosestNumbers(int[] A, int target, int k) {
        // Write your code here
        if (A == null || A.length < k || k <= 0) {
            return new int[0];
        }

        int[] result = new int[k];

        int start = 0;
        int end = A.length;

        while (start < end - 1) {
            int mid = start + (end - start) / 2;
            if (A[mid] >= target) {
                end = mid;
            } else {
                start = mid;
            }
        }

        int startIndex = Math.max(0, start - k + 1);
        int endIndex = Math.min(A.length - 1, end + k - 1);

        for (int i = 0; i < k; i++) {
            int startDiff = (start < 0) ? Integer.MAX_VALUE : Math.abs(A[start] - target);
            int endDiff = (end >= A.length) ? Integer.MAX_VALUE : Math.abs(A[end] - target);
            if (startDiff <= endDiff) {
                result[i] = A[start];
                start--;
            } else {
                result[i] = A[end];
                end++;
            }

        }

        return result;
    }
}
```
