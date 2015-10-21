##Rotate String

21% Accepted

	Given a string and an offset, rotate string by offset. (rotate from left to right)

	Have you met this question in a real interview? Yes
	Example
	Given "abcdefg".

	offset=0 => "abcdefg"
	offset=1 => "gabcdef"
	offset=2 => "fgabcde"
	offset=3 => "efgabcd"

####Challenge
- Rotate in-place with O(1) extra memory.

####Tags Expand
- String

####思路
- 三次翻转
- reverse函数里边 用i,j，而没有在[]写入复杂的表达式 逻辑性更强






```java
public class Solution {
    /**
     * @param str: an array of char
     * @param offset: an integer
     * @return: nothing
     */
    public void rotateString(char[] str, int offset) {
        // write your code here
        if( str == null || str.length == 0){
            return;
        }

        int len = str.length;
        offset = offset % len;

        reverse(str, 0, len - 1);
        reverse(str, 0 , offset - 1);
        reverse(str, offset, len - 1);

    }

    private void reverse(char[] A, int start, int end) {
            for (int i = start, j = end; i < j; i++, j--) {
                char temp = A[i];
                A[i] = A[j];
                A[j] = temp;
            }
        }
}

```
