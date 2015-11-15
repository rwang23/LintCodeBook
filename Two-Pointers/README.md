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

####并行型
- 两个数组
- 用于 merger two linked list这种
