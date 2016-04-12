##Group Shifted Strings

	Total Accepted: 8470 Total Submissions: 27003 Difficulty: Easy
	Given a string, we can "shift" each of its letter to its successive letter, for example: "abc" -> "bcd". We can keep "shifting" which forms the sequence:

	"abc" -> "bcd" -> ... -> "xyz"
	Given a list of strings which contains only lowercase alphabets, group all strings that belong to the same shifting sequence.

	For example, given: ["abc", "bcd", "acef", "xyz", "az", "ba", "a", "z"],
	Return:

	[
	  ["abc","bcd","xyz"],
	  ["az","ba"],
	  ["acef"],
	  ["a","z"]
	]
	Note: For the return value, each inner list's elements must follow the lexicographic order.

####思路
- [参考](http://blog.csdn.net/pointbreak1/article/details/48780345)
- 用一个hashtable去存string pattern,这个string pattern作为key,然后他对应的strings们作为value
- 怎么去找这个string pattern呢?
- 可以有很多方法,比如找string里边跟第一个字母的距离,或者每个字符的距离
- 还有一个容易错的地方,就是遇到超出了z之后又重头开始的情况,比如yza
- 这个时候,可以((a - y) + 26) % 26
- ["eqdf", "qcpr"]。
- ((‘q’ - 'e') + 26) % 26 = 12, ((‘d’ - 'q') + 26) % 26 = 13, ((‘f’ - 'd') + 26) % 26 = 2
- ((‘c’ - 'q') + 26) % 26 = 12, ((‘p’ - 'c') + 26) % 26 = 13, ((‘r’ - 'p') + 26) % 26 = 2

```java
public class Solution {
    public List<List<String>> groupStrings(String[] strings) {
        List<List<String>> result = new ArrayList<List<String>>();
        HashMap<String, List<String>> d = new HashMap<>();
        for(int i = 0; i < strings.length; i++) {
            StringBuffer sb = new StringBuffer();
            for(int j = 0; j < strings[i].length(); j++) {
                sb.append(Integer.toString(((strings[i].charAt(j) - strings[i].charAt(0)) + 26) % 26));
                sb.append(" ");
            }
            String shift = sb.toString();
            if(d.containsKey(shift)) {
                d.get(shift).add(strings[i]);
            } else {
                List<String> l = new ArrayList<>();
                l.add(strings[i]);
                d.put(shift, l);
            }
        }

        for(String s : d.keySet()) {
            Collections.sort(d.get(s));
            result.add(d.get(s));
        }
        return result;
    }
}
```
