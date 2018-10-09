##K Closest Points

  Given some points and a point origin in two dimensional space, 
  find k points out of the some points which are nearest to origin.
  Return these points sorted by distance, if they are same with distance, sorted by x-axis, otherwise sorted by y-axis.

##Example
  Given points = [[4,6],[4,7],[4,4],[2,5],[1,1]], origin = [0, 0], k = 3
  return [[1,1],[2,5],[4,4]]
 
 
##解法

```java
/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */

public class Solution {
    /**
     * @param points: a list of points
     * @param origin: a point
     * @param k: An integer
     * @return: the k closest points
     */
    public Point[] kClosest(Point[] points, Point origin, int k) {
        // write your code here
        if (points == null || points.length == 0 || k <= 0) {
            return new Point[0];
        }
        
        Point[] result = new Point[k];
        
        Arrays.sort(points, new Comparator<Point>(){
            public int compare(Point A, Point B) {
                double distanceA = Math.pow(Math.abs(A.x - origin.x), 2) + Math.pow(Math.abs(A.y - origin.y), 2);
                double distanceB = Math.pow(Math.abs(B.x - origin.x), 2) + Math.pow(Math.abs(B.y - origin.y), 2);
                
                if (distanceA == distanceB) {
                    if (A.x != B.x) {
                        return A.x - B.x;
                    } else {
                        return A.y - B.y;
                    }
                }
                
                return Double.compare(distanceA, distanceB);
            }
        });
        
        for (int i = 0; i < k; i++) {
            result[i] = points[i];
        }
        
        return result;
    }
}
```
