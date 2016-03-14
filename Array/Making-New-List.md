##Making New List
	there is a list contains n students'id/
	making a new list from this list, starting from taking out the dth student
	until the original is empty

				   old   new
	at first    12345
	first time  1235      4
	second time 123       45
	third time  12        453
	fourth      1         4532
	last time             45321

####O(n2)暴力解法

```java
import java.util.ArrayList;


public class Solution {

	public ArrayList<Integer> put(ArrayList<Integer> input, int d) {

		ArrayList<Integer> newList = new ArrayList<Integer>();
		while (input.size() != 0) {
			int size = input.size();
			ArrayList<Integer> index = new ArrayList<Integer>();
			for (int i = 0; i < size; i++) {
				if ((i + 1) % d == 0) {
					newList.add(input.get(i));
					index.add(input.get(i));
				}
			}
			for (int i = 0; i < index.size(); i++) {
				input.remove(index.get(i));
			}

			if (size < d) {
				for (int i = size - 1; i >= 0; i--) {
					newList.add(input.get(i));
				}
				return newList;
			}
		}
		return newList;
	}

    public static void main(String[] args) {
    	Solution sol = new Solution();
    	ArrayList<Integer> input = new ArrayList<Integer>();
    	input.add(1);
    	input.add(2);
    	input.add(3);
    	input.add(4);
    	input.add(5);
    	input.add(6);
    	input.add(7);
    	input.add(8);

    	ArrayList<Integer> result = sol.put(input, 4);
    	for (int i = 0; i < result.size(); i++) {
    		System.out.print(result.get(i) +" ");
    	}
    	System.out.println("done");

    }
}

###可以改用linkedlist来解

