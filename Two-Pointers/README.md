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

