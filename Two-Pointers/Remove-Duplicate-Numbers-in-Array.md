##Remove Duplicate Numbers in Array
Given an array of integers, remove the duplicate numbers in it.

  You should:

  Do it in place in the array.
  Move the unique numbers to the front of the array.
  Return the total number of the unique numbers.

###Example
  Given nums = [1,3,1,4,4,2], you should:

  Move duplicate integers to the tail of nums => nums = [1,3,4,2,?,?].
  Return the number of unique integers in nums => 4.
  Actually we don't care about what you place in ?, we only care about the part which has no duplicate integers.

###Challenge
  Do it in O(n) time complexity.
  Do it in O(nlogn) time without extra space.
  Notice
  You don't need to keep the original order of the integers.
  
###思路1
- 解决O(n) time complexity
- 使用一个map就行

```java
public int deduplication(int[] nums) {
        // Write your code here
        HashMap<Integer, Boolean> mp = new HashMap<Integer, Boolean>();
        for (int i = 0; i < nums.length; ++i)
            mp.put(nums[i], true);

        int result = 0;
        for (Map.Entry<Integer, Boolean> entry : mp.entrySet())
            nums[result++] = entry.getKey();
        return result;
    }
```
###思路2
- 先排序
- 再两根指针，需要着重掌握
- 由于根本不管后面的重复元素放不放在后面，只需要保证unique的元素放在前面就行
- 一根指针向右走找相同的元素，一根指针就指向当前该写的元素
- 自己写的时候把很简单的问题写得却很复杂

```java
 public int deduplication(int[] nums) {
        if (nums.length == 0) {
            return 0;
        }
        
        Arrays.sort(nums);
        int len = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != nums[len]) {
                nums[++len] = nums[i];
            }
        }
        return len + 1;
    }
```
