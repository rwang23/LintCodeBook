##Two Pointers

两根指针模板

        int start = 0;
        int end = A.length - 1;
        while (start <= end) {
            while (start <= end && A[start] != elem) {
                start++;
            }
            while (start <= end && A[end] == elem) {
                end--;
            }
            if (start <= end) {
                exch(A, start, end);
                start++;
                end--;
            }
        }

[很好的参考资料](http://blog.csdn.net/ohmygirl/article/details/7850068)

####对撞型
- 一个数组,两边向中间移动
- 用于two sum类型 water类 Partition类
- 通过对撞型指针优化算法,根本就是证明不用扫描多余的状态

####前向型
- 一个数组,同时向前
- 用于 窗口类,快慢指针类
- 也就是不用多扫描多余的状态

####模板
自己写的时候,无非就是条件变化而已
先写暴力解法,再根据暴力解法优化即可

```java
public int minimumSize(int[] nums, int s) {
    // write your code here
    /*
    异常判断
     */
    */
    if (nums == null || nums.length == 0) {
        return -1;
    }

    int size = nums.length;
    int min = Integer.MAX_VALUE;
    int sum = 0;
    int length = 0;
    /*
    开始i的循环,
    j <= size, 因为自己在写j的时候,j++
     */
    for (int i = 0,  j = 0; i < size && j <= size; i++) {
        /*
        在i == 0的时候,不作为
        i != 0 的时候,相当于i进入了下一层 比如[0,3] 进入到 [1,3], 要删除[0]的状态
         */
        if (i != 0) {
            sum = sum - nums[i-1];
            length--;
        }

        /*
        指针J 开始作用,
        判断j 首先 j <size && 导致会满足题意的条件
        长度length++
         */
        while (sum < s && j < size) {
            sum = sum + nums[j++];
            length++;
        }

        /*
        最终判断,看是不是符合条件,
        因为有的循环完了,也没有找到合适的
         */
        if (sum >= s) {
            min = Math.min(min, length);
        }

    }
    /*
    如果min都没变,说明根本没找到, 返回-1
     */
    return min == Integer.MAX_VALUE ? -1 : min;

}
```
####并行型
- 两个数组
- 用于 merger two linked list这种
