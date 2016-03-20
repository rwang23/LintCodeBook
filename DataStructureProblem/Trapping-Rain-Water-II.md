##Trapping Rain Water II

	Given n x m non-negative integers representing an elevation map 2d
	where the area of each cell is 1 x 1,
	compute how much water it is able to trap after raining.



	Have you met this question in a real interview? Yes
	Example
	Tags
	Related Problems
	 Notes
	Given 5*4 matrix

	[12,13,0,12]
	[13,4,13,12]
	[13,8,10,12]
	[12,13,12,12]
	[13,13,13,13]

####思路
- 使用min heap时间复杂度为 O(mnlogmn)
- 思路来自I的加强,在I里边,使用了两根指针夹击,根本原因还是因为木桶原理,低的一边会漏水,所以会从低点入手
- II也是同样如此,但是变成了二维的了
- 但是我们还是要找最低点,如果最快的获取最低点就成了难点
- 首先给点设置了一个类
- 然后想到了放在min heap里边,这样就能快速获得最低点,首先把最外层放进heap,然后找到最低点不断向里边夹击
- 访问之后再移除该点,当min heap没有元素的时候就说明访问完毕,得到了答案
- 访问的时候,不能访问已经访问过的点以及超出边界的点了,所以设置了条件
- 如果访问的点的高度更低,说明有水,就进行累加,把新点放进来的时候,放的是外围点的高度

```java
public class Solution {
    /**
     * @param heights: a matrix of integers
     * @return: an integer
     */

    private class Node{
        private int height;
        private int x;
        private int y;
        Node(int height, int x, int y) {
            this.height = height;
            this.x = x;
            this.y = y;
        }
    }
    public int trapRainWater(int[][] heights) {
        // write your code here
        if (heights == null || heights.length == 0 || heights[0].length == 0) {
            return 0;
        }
        int m = heights.length;
        int n = heights[0].length;
        PriorityQueue<Node> pq = new PriorityQueue<Node>(11, new Comparator<Node>(){
            public int compare(Node n1, Node n2) {
                return n1.height - n2.height;
            }
        });

        int[][] isVisited = new int[m][n];

        for (int i = 0; i < n; i++) {
            Node node = new Node(heights[0][i], 0, i);
            pq.offer(node);
            isVisited[0][i] = 1;
            node = new Node(heights[m - 1][i], m - 1, i);
            pq.offer(node);
            isVisited[m - 1][i] = 1;
        }

        for (int i = 1; i < m; i++) {
            Node node = new Node(heights[i][0], i, 0);
            pq.offer(node);
            isVisited[i][0] = 1;
            node = new Node(heights[i][n - 1], i, n - 1);
            pq.offer(node);
            isVisited[i][n - 1] = 1;
        }

        int volume = 0;
        int[] xStep = new int[]{0, 0, -1, 1};
        int[] yStep = new int[]{-1, 1, 0, 0};

        while (!pq.isEmpty()) {
            Node cur = pq.poll();
            for (int k = 0; k < 4; k++) {
                int newX = cur.x + xStep[k];
                int newY = cur.y + yStep[k];
                if (newX >= m || newY >= n || newX < 0 || newY < 0 || isVisited[newX][newY] == 1) {
                    continue;
                }
                isVisited[newX][newY] = 1;

                if (heights[newX][newY] < cur.height) {
                    volume += cur.height - heights[newX][newY];
                    pq.offer(new Node(cur.height, newX, newY));
                } else {
                    pq.offer(new Node(heights[newX][newY], newX, newY));
                }
            }
        }

        return volume;

    }
};

```
