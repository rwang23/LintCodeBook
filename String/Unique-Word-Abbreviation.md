##Unique Word Abbreviation
	Total Accepted: 6495 Total Submissions: 41761 Difficulty: Easy
	An abbreviation of a word follows the form <first letter><number><last letter>. Below are some examples of word abbreviations:

	a) it                      --> it    (no abbreviation)

	     1
	b) d|o|g                   --> d1g

	              1    1  1
	     1---5----0----5--8
	c) i|nternationalizatio|n  --> i18n

	              1
	     1---5----0
	d) l|ocalizatio|n          --> l10n
	Assume you have a dictionary and given a word, find whether its abbreviation is unique in the dictionary. A word's abbreviation is unique if no other word from the dictionary has the same abbreviation.

	Example:
	Given dictionary = [ "deer", "door", "cake", "card" ]

	isUnique("dear") -> false
	isUnique("cart") -> true
	isUnique("cane") -> false
	isUnique("make") -> true

####思路
- 注意["hello"],isUnique("hello") 是返回的true, hello是unique的单词
- 所以使用hashmap的时候要注意一下,如果key只对应一个,就放入这个string,如果多个,自然是无效的,设置为null
- 然后对比isUnique的时候,判断,首先是不是无效的,然后判断key对应的string是不是一致的

```java
public class ValidWordAbbr {
    HashMap<String, String> map;
    public ValidWordAbbr(String[] dictionary) {
        map = new HashMap<String, String>();
        for(String str:dictionary){
            String key = getKey(str);
            // If there is more than one string belong to the same key
            // then the key will be invalid, we set the value to ""
            if(map.containsKey(key)){
                if(!map.get(key).equals(str)){
                    map.put(key, "");
                }
            }
            else{
                map.put(key, str);
            }
        }
    }

    public boolean isUnique(String word) {
        return !map.containsKey(getKey(word))||map.get(getKey(word)).equals(word);
    }

    String getKey(String str){
        if(str.length()<=2) return str;
        return str.charAt(0)+Integer.toString(str.length()-2)+str.charAt(str.length()-1);
    }
}
```
