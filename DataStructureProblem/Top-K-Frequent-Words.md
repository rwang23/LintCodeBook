##Top K Frequent Words

	Given a list of words and an integer k,
	return the top k frequent words in the list.

	Have you met this question in a real interview? Yes
	Example
	Given

	[
	    "yes", "lint", "code",
	    "yes", "code", "baby",
	    "you", "baby", "chrome",
	    "safari", "lint", "code",
	    "body", "lint", "code"
	]
	for k = 3, return ["code", "lint", "baby"].

	for k = 4, return ["code", "lint", "baby", "yes"],

	Note
	You should order the words by the frequency of them in the return list,
	the most frequent one comes first. If two words has the same frequency, the one with lower alphabetical order come first.

####Challenge
Do it in O(nlogk) time and O(n) extra space.

Extra points if you can do it in O(n) time with O(k) extra space.

####Tags Expand
Hash Table Heap Priority Queue


####思路
- 利用Priority queue来排序(建立一个自己的类,先通过times,再通过字母顺序排)
- 先扫描各个单词的数目,使用Hashmap,因为这样在读取的时候只使用了o(1)的时间
- 还有一个关键是,遍历hashmap
- Map.Entry<String, Integer> entry : map.entrySet()
- entry.getKey() entry.getValue()

```java
public class Solution {
    /**
     * @param words an array of string
     * @param k an integer
     * @return an array of string
     */
    class Element {
        int times;
        String word;
        Element(int times, String word) {
            this.times = times;
            this.word = word;
        }
    }

    private Comparator<Element> sort = new Comparator<Element>() {
        public int compare(Element a, Element b) {
            if (a.times == b.times) {
                String worda = a. word;
                String wordb = b.word;
                return worda.compareTo(wordb);
            } else {
                return b.times - a.times;
            }
        }
    };

    public String[] topKFrequentWords(String[] words, int k) {
        // Write your code here
        if (words == null || k < 0 || words.length < k) {
            return new String[0];
        }
        PriorityQueue<Element> pq = new PriorityQueue<Element>(words.length, sort);
        HashMap<String, Integer> map = new HashMap<String, Integer>();
        String[] result = new String[k];

        for (String word: words) {
            if (map.containsKey(word)) {
                int times = map.get(word);
                map.put(word, times + 1);
            } else {
                map.put(word, 1);
            }
        }
        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            String key = entry.getKey();
            int value = entry.getValue();
            Element cur = new Element(value, key);
            pq.offer(cur);
        }

        for (int i = 0; i < k; i++) {
            result[i] = pq.poll().word;
        }

        return result;
    }
}

```
