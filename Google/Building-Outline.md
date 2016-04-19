##Building Outline


	Given N buildings in a x-axis，each building is a rectangle and can be represented by a triple (start, end, height)，where start is the start position on x-axis, end is the end position on x-axis and height is the height of the building. Buildings may overlap if you see them from far away，find the outline of them。

	An outline can be represented by a triple, (start, end, height), where start is the start position on x-axis of the outline, end is the end position on x-axis and height is the height of the outline.

	Building Outline

	Have you met this question in a real interview? Yes
	 Notice

	Please merge the adjacent outlines if they have the same height and make sure different outlines cant overlap on x-axis.

	Example
	Tags
	Related Problems
	 Notes
	Given 3 buildings：

	[
	  [1, 3, 3],
	  [2, 4, 4],
	  [5, 6, 1]
	]
	The outlines are：

	[
	  [1, 2, 3],
	  [2, 4, 4],
	  [5, 6, 1]
	]


####思路
- 一看就是scan-line
- 但是要寻找最大高度,这个时候引入了heap
- 所以是scan-line + heap
- 注意比较两个Integer的时候,不能直接 ==, 而是要用 intValue(),自己在这里卡了两个小时debug,其实很简单嘛

```java
public class Solution {
    /**
     * @param buildings: A list of lists of integers
     * @return: Find the outline of those buildings
     */

    private class MyNode {

        private int position;
        private int status;
        private int id;

        /*
        * status == 1 means it is end point, status == 0 means it is start point
        */
        MyNode(int position, int status, int id) {
            this.position = position;
            this.status = status;
            this.id = id;
        }
    }
    public ArrayList<ArrayList<Integer>> buildingOutline(int[][] buildings) {
        // write your code here
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
        if (buildings == null || buildings.length == 0 || buildings[0].length != 3) {
            return result;
        }

        PriorityQueue<Integer> pq = new PriorityQueue<Integer>(11, Collections.reverseOrder());
        List<MyNode> list = new ArrayList<MyNode>();
        for (int i = 0; i < buildings.length; i++) {
            for (int j = 0; j < buildings[0].length; j++) {
                int start = buildings[i][0];
                int end = buildings[i][1];
                MyNode firstNode = new MyNode(start, 0, i);
                MyNode nextNode = new MyNode(end, 1, i);
                list.add(firstNode);
                list.add(nextNode);
            }
        }

        Collections.sort(list, new Comparator<MyNode>(){
            public int compare(MyNode n1, MyNode n2) {
                if (n1.position == n2.position) {
                    return n2.status - n1.status;
                } else {
                    return n1.position - n2.position;
                }
            }
        });

        for (int i = 0; i + 1 < list.size(); i++) {

            ArrayList<Integer> outline = new ArrayList<Integer>();
            MyNode firstNode = list.get(i);
            int id = firstNode.id;
            if (firstNode.status == 1) {
                pq.remove(buildings[id][2]);
            } else {
                pq.offer(buildings[id][2]);
            }

            if (pq.isEmpty()) {
                continue;
            }

            outline.add(firstNode.position);
            int height = pq.peek();
            MyNode nextNode = list.get(i + 1);
            outline.add(nextNode.position);
            outline.add(height);

            if (outline.get(0) == outline.get(1)) {
                continue;
            }

            int size = result.size();
            if (size >= 1) {
                ArrayList<Integer> pre = result.get(size - 1);
                if (outline.get(0).intValue() == pre.get(1).intValue() && outline.get(2).intValue() == pre.get(2).intValue()) {
                    outline.set(0, pre.get(0));
                    result.remove(size - 1);
                }
            }

            result.add(outline);

        }

        return result;
    }
}

```
