###Compress String

```java
/*
aaabb -> a3b2
 */

/*
test case
aaabb

result -> a3
size = 5
i = 0, j = 1, c = 1
j = 2 c = 2
j = 3 c = 3 j - > b

c = 1, i = 3, j = 4
j = 5 c = 2

 */
public class solution{

	public String compressString(String input) {
		if (input == null || input.length() <= 1) {
			return input;
		}

		int size = input.length();
		int i = 0;
		int j = 1;
		int count = 1;
		StringBuilder result = new StringBuilder();

		while (j < size) {
			count = 1;
			while (j < size && input.charAt(i) == input.charAt(j)) {
				j++;
				count++;
			}

			result.append(input.charAt(i));
			result.append(Integer.toString(count));
			i = j;
			j++;
		}
		return result.toString();

	}
}


```
