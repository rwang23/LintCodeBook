##Smallest Rectangle Enclosing Black Pixels

	Total Accepted: 4218 Total Submissions: 10835 Difficulty: Hard
	An image is represented by a binary matrix with 0 as a white pixel and 1 as a black pixel.
	The black pixels are connected, i.e., there is only one black region.
	Pixels are connected horizontally and vertically. Given the location (x, y) of one of the black pixels,
	return the area of the smallest (axis-aligned) rectangle that encloses all black pixels.

	For example, given the following image:

	[
	  "0010",
	  "0110",
	  "0100"
	]
	and x = 0, y = 2,
	Return 6.

####思路
- O(mn)暴力扫一遍,留下left right top bottom的值,然后计算
- BFS/DFS 从给的点入手, O(k)

```java
public class Solution {
    private class Point {
        private int x;
        private int y;
        Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }
    public int minArea(char[][] image, int x, int y) {
        if (image == null || image.length == 0 || image[0].length == 0) {
            return 0;
        }
        int m = image.length;
        int n = image[0].length;
        if (x >= m || y >= n) {
            return 0;
        }

        int[] xstep = new int[]{0, 0, 1, -1};
        int[] ystep = new int[]{1, -1, 0, 0};

        int left = n - 1;
        int top = m - 1;
        int right = 0;
        int bottom = 0;

        Queue<Point> queue = new LinkedList<Point>();
        queue.offer(new Point(x,y));

        while (!queue.isEmpty()) {
            Point cur = queue.poll();

            x = cur.x;
            y = cur.y;
            left = Math.min(left, y);
            top = Math.min(top, x);
            right = Math.max(right, y);
            bottom = Math.max(bottom, x);

            for (int i = 0; i < 4; i++) {
                int newX = x + xstep[i];
                int newY = y + ystep[i];
                if (newX >= 0 && newY >= 0 && newX < m && newY < n && image[newX][newY] == '1') {
                    queue.offer(new Point(newX, newY));
                    image[newX][newY] = '0';
                }
            }
        }

        return (right - left + 1) * (bottom - top + 1);
    }
}
```

####Binary Search
[参考](https://leetcode.com/problems/smallest-rectangle-enclosing-black-pixels/)

```java
public class Solution {
    private char[][] image;
    public int minArea(char[][] iImage, int x, int y) {
        image = iImage;
        int m = image.length, n = image[0].length;
        int left = searchColumns(0, y, 0, m, true);
        int right = searchColumns(y + 1, n, 0, m, false);
        int top = searchRows(0, x, left, right, true);
        int bottom = searchRows(x + 1, m, left, right, false);
        return (right - left) * (bottom - top);
    }
    private int searchColumns(int i, int j, int top, int bottom, boolean opt) {
        while (i != j) {
            int k = top, mid = (i + j) / 2;
            while (k < bottom && image[k][mid] == '0') ++k;
            if (k < bottom == opt)
                j = mid;
            else
                i = mid + 1;
        }
        return i;
    }
    private int searchRows(int i, int j, int left, int right, boolean opt) {
        while (i != j) {
            int k = left, mid = (i + j) / 2;
            while (k < right && image[mid][k] == '0') ++k;
            if (k < right == opt)
                j = mid;
            else
                i = mid + 1;
        }
        return i;
    }
}
```
