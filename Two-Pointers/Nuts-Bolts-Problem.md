##Nuts & Bolts Problem

12% Accepted

	Given a set of n nuts of different sizes and n bolts of different sizes.
	There is a one-one mapping between nuts and bolts.
	Comparison of a nut to another nut or a bolt to another bolt is not allowed.
	It means nut can only be compared with bolt and bolt can only be compared with nut to see which one is bigger/smaller.

	We will give you a compare function to compare nut with bolt.

	Have you met this question in a real interview? Yes
	Example
	Given nuts = ['ab','bc','dd','gg'], bolts = ['AB','GG', 'DD', 'BC'].

	Your code should find the matching bolts and nuts.

	one of the possible return:

	nuts = ['ab','bc','dd','gg'], bolts = ['AB','BC','DD','GG'].

	we will tell you the match compare function. If we give you another compare function.

	the possible return is the following:

	nuts = ['ab','bc','dd','gg'], bolts = ['BC','AA','DD','GG'].

	So you must use the compare function that we give to do the sorting.

	The order of the nuts or bolts does not matter. You just need to find the matching bolt for each nut.

####Tags Expand
- Quick Sort Sort

####思路
- 不难
- 首先使用 nuts 中的某一个元素作为基准对 bolts 进行 partition 操作，随后将 bolts 中得到的基准元素作为基准对 nuts 进行 partition 操作。
- 找pivot遍历就行
- 题有问题,不用重做,看思想就可
- 难以理解的可能在partition部分，不仅需要使用compare.cmp(alist[i], pivot), 同时也需要使用compare.cmp(pivot, alist[i]), 否则答案有误。
- Because `compare.cmp(str[i], pivot) == -1` may not identical to `compare.cmp(pivot, str[i]) == 1`, we can not see the detailed implementation of `cmp` method.


```java
/**
 * public class NBCompare {
 *     public int cmp(String a, String b);
 * }
 * You can use compare.cmp(a, b) to compare nuts "a" and bolts "b",
 * if "a" is bigger than "b", it will return 1, else if they are equal,
 * it will return 0, else if "a" is smaller than "b", it will return -1.
 * When "a" is not a nut or "b" is not a bolt, it will return 2, which is not valid.
*/
public class Solution {

    public void sortNutsAndBolts(String[] nuts, String[] bolts, NBComparator compare) {
        sortSubArray(nuts, bolts, 0, nuts.length - 1, compare);
    }

    private void sortSubArray(String[] nuts, String[] bolts, int start, int end, NBComparator compare) {
        if (start >= end) return;
        int pivot = partition1(nuts[start], bolts, start, end, compare);
        partition2(bolts[pivot], nuts, start, end, compare);
        sortSubArray(nuts, bolts, start, pivot - 1, compare);
        sortSubArray(nuts, bolts, pivot + 1, end, compare);
    }

    private int partition1(String item, String[] arrays, int start, int end, NBComparator compare) {

        int left = start;
        int right = end;

        while (true) {
            while (compare.cmp(item, arrays[left]) < 0) {
                if(left == end) break;
                left++;
            }
            while (compare.cmp(item, arrays[right]) > 0) {
                if(right == start) break;
                right--;
            }

            if (left >= right) break;
            swap(arrays, left, right);
        }

        for (int i = start; i <= end; i++ ) {
            if(compare.cmp(item, arrays[i]) == 0) left = i;
        }
        return left;
    }

    private int partition2(String item,String[] arrays, int start, int end, NBComparator compare){
        int left = start;
        int right = end;

        while (true) {
            while (compare.cmp(arrays[left], item) > 0) {
                if(left == end) break;
                left ++;
            }
            while (compare.cmp(arrays[right], item) < 0) {
                if(right == start) break;
                right --;
            }
            if (left >= right) break;
            swap(arrays, left, right);
        }
        for (int i = start; i <= end; i++ ) {
            if(compare.cmp(item, arrays[i]) == 0) left = i;
        }
        return left;
    }

    private void swap(String[] array, int a, int b){
        String temp = array[a];
        array[a] = array[b];
        array[b] = temp;
    }
};


```
