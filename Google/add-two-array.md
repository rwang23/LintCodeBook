###Add two array

add elements of two array

```java
/*
 1 2 3 4 5
     1 5 5
1 2 5 0 0
 */


/*
test case

1 2 3 4 5
1 5 5

result = 13500
min = 3
max = 5
longer = input1
short = input2
carry = 0
sum = 10
carry = 1;
digit = 0;

 */


public class Solution{
	public int[] add(int[] input1, int[] input2) {
		int m = input1.length;
		int n = input2.length;

		int min = Math.min(m, n);
		int max = Math.max(m, n);

		int[] longer;
		int[] shorter;
		if (max == m) {
			longer = input1;
			shorter = input2;
		} else {
			longer = input2;
			shorter = input1;
		}
		int carry = 0;
		ArrayList<Integer> result = new ArrayList<Integer>();


		for (int i = min - 1, j = max - 1; i >= 0; i--) {
			int sum = longer[i] + shorter[i] + carry;
			int digit = sum % 10;
			carry = sum / 10;
			result.add(0, digit);
		}

		for (int i = max - min - 1; i >= 0; i--) {
			int sum = longer[i] + carry;
			int digit = sum % 10;
			carry = sum / 10;
			result.add(0, digit);
		}

		int digit = carry;
		if (digit != 0) {
			result.add(0, digit);
		}

		int size = result.size();
		int[] output = new int[size];
		for (int i = 0; i < size; i++) {
			output[i] = result.get(i);
		}

		return output;

	}
}

```
