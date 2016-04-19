```java

import java.util.HashMap;
import java.util.Map;

public class Solution {
	public int AnyToDec (String input, int k) {
		//considering valid string input
		if (input == null || input.equals("") || k > 36) {
			throw new IllegalArgumentException("input is not valid");
		}

		int result = 0;
		int size = input.length();
		Map<Character, Integer> map = new HashMap<Character, Integer>();
		int base = 10;
		for (int i = 0; i < k - 10; i++) {
			char cur = (char)('a' + i);
			map.put(cur, base++);
		}

		for (int i = 0; i < size; i++) {
			result *= k;
			char cur = input.charAt(i);
			if (map.containsKey(cur)) {
				result += map.get(cur);
			} else {
				if (cur >= '0' && cur < '9' && cur < (char)(k + '0')) {
					result += cur - '0';
				} else {
					throw new IllegalArgumentException("input is not valid");
				}
			}
		}

		return result;
	}

	public static void main(String[] args) {
		Solution sol = new Solution();
		int res = sol.AnyToDec("1000", 2);
		System.out.println(res);
	}
}
```
