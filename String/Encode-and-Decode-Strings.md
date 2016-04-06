##Encode and Decode Strings

	Total Accepted: 6210 Total Submissions: 23025 Difficulty: Medium
	Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.

	Machine 1 (sender) has the function:

	string encode(vector<string> strs) {
	  // ... your code
	  return encoded_string;
	}
	Machine 2 (receiver) has the function:
	vector<string> decode(string s) {
	  //... your code
	  return strs;
	}
	So Machine 1 does:

	string encoded_string = encode(strs);
	and Machine 2 does:

	vector<string> strs2 = decode(encoded_string);
	strs2 in Machine 2 should be the same as strs in Machine 1.

	Implement the encode and decode methods.

	Note:
	The string may contain any possible characters out of 256 valid ascii characters.
	Your algorithm should be generalized enough to work on any possible characters.
	Do not use class member/global/static variables to store states.
	Your encode and decode algorithms should be stateless.
	Do not rely on any library method such as eval or serialize methods.
	You should implement your own encode/decode algorithm.

####思路
- 如何加密是个难题
- 直接用一个len长度,看上去可以,但是长度这个字符也可能重了
- 所以加上len 在加上一个特殊字符,这样通过Len的长度就能提取出一个字符串
- 值得注意的是如果一个string == null,那么是不能用string.size()会出runtime error
- 同时这个len可能是多位数,不能通过一位digit就能判断出来,要通过一个substring

```java
public class Codec {

    // Encodes a list of strings to a single string.
    public String encode(List<String> strs) {
        if (strs == null || strs.size() == 0) {
            return new String();
        }

        StringBuilder string = new StringBuilder();
        for (int i = 0; i < strs.size(); i++) {
            String cur = strs.get(i);
            if (cur != null) {
                int len = cur.length();
                string.append(len);
                string.append('#');
                string.append(cur);
            } else {
                string.append(0);
                string.append('#');
            }
        }
        return string.toString();
    }

    // Decodes a single string to a list of strings.
    public List<String> decode(String s) {
        if (s == null) {
            return new ArrayList<String>();
        }
        List<String> result = new ArrayList<String>();
        int size = s.length();
        int j = 0;
        while (j < size) {
            int i = j;
            char first = s.charAt(j);
            while (Character.isDigit(s.charAt(j))) {
                j++;
            }
             char second = s.charAt(j);
            int len = 0;
            int num = Integer.parseInt(s.substring(i, j));

            if (Character.isDigit(first) && second == '#') {
                if (first == '0' && second == '#') {
                    result.add(new String());
                } else {
                    len = num;
                    String cur = s.substring(j + 1, j + 1 + len);
                    result.add(cur);
                }
            }
            j = j + 1 + len;
        }

        return result;

    }
}

```
