```java

import java.util.HashMap;
import java.util.Map;

public class Solution {
	public int hexToDec (String input) {
		//considering valid string input
		if (input == null || input.equals("")) {
			throw new IllegalArgumentException("input is not valid");
		}

		int result = 0;
		int size = input.length();
		Map<Character, Integer> map = new HashMap<Character, Integer>();
		map.put('a', 10);
		map.put('b', 11);
		map.put('c', 12);
		map.put('d', 13);
		map.put('e', 14);
		map.put('f', 15);

		for (int i = 0; i < size; i++) {
			result *= 16;
			char cur = input.charAt(i);
			if (map.containsKey(cur)) {
				result += map.get(cur);
			} else {
				result += cur - '0';
			}
		}

		return result;
	}

	public static void main(String[] args) {
		Solution sol = new Solution();
		int res = sol.hexToDec("435fae");
		System.out.println(res);
	}
}
```
