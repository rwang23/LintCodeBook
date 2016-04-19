##Much Larger Numbers

	Input : an array of integers
	Output: *index* of the "Much Larger" number, or -1 if there is no such number.

	A number is "Much Larger" if it is more than twice every other value in the array.


	1,6,19,9: should return "2", the index of 19
	1,11,6,9: should return "-1", because there is no "Much Larger" number.
	1,19,19,9: should return "-1", because there is no single value that is "much larger".


####思路
- 一个是过一遍找最大值再比较
- 一个是one for loop就解决, 找second max

```java
public class MuchLargetNum {

	public int muchLarger(int[] input) {
		if (input == null || input.length == 0) {
			return -1;
		}

		int maxNumber = input[0];
		//int countMax = 1;
		int indexOfMax = 0;
		int n = input.length;

		for (int i = 1; i< n; i++) {
			if (input[i] == maxNumber) {
				//countMax++;
			} else if (input[i] >= maxNumber) {
				maxNumber =input[i];
				indexOfMax = i;
				// countMax = 1;
			}
		}

	//if (countMax > 1) {
	//	return -1;
	//}

		for (int i = 0; i < n; i++) {
			if (indexOfMax == i) {
			continue;
			} else {
				if ((maxNumber / 2.0) <= (input[i])){
					return -1;
				}
			}
		}
			return indexOfMax;
	}
}
```
