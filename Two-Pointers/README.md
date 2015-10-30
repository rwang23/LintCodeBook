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
