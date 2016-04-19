##Add and Search Word - Data structure design

	Total Accepted: 21721 Total Submissions: 107141 Difficulty: Medium
	Design a data structure that supports the following two operations:

	void addWord(word)
	bool search(word)
	search(word) can search a literal word or a regular expression string containing only letters a-z or .. A . means it can represent any one letter.

	For example:

	addWord("bad")
	addWord("dad")
	addWord("mad")
	search("pad") -> false
	search("bad") -> true
	search(".ad") -> true
	search("b..") -> true

####思路
- Trie Tree
- 遇到点的时候无非也就是忽略这个点,找下面26个根节点,只要一个符合就可以了

```java
public class WordDictionary {
    private class Node {
        private Node[] next;
        private int value;
        Node() {
            next = new Node[26];
            value = 0;
        }
    }

    private Node root = new Node();

    // Adds a word into the data structure.
    public void addWord(String word) {
        addWord(root, word, 0, 1);
    }

    public Node addWord(Node root, String word, int index, int value) {
        if (root == null) {
            root = new Node();
        }

        if (word.length() == index) {
            root.value = value;
            return root;
        }

        int c = word.charAt(index) - 'a';
        root.next[c] = addWord(root.next[c], word, index + 1, value);
        return root;
    }

    // Returns if the word is in the data structure. A word could
    // contain the dot character '.' to represent any one letter.
    public boolean search(String word) {
        return search(root, word, 0);
    }

    public boolean search(Node root, String word, int index) {
        if (root == null) {
            return false;
        }

        if (word.length() == index && root.value != 0) {
            return true;
        }

        if (word.length() == index && root.value == 0) {
            return false;
        }

        boolean isValid = false;
        if (word.charAt(index) == '.') {
            for (int c = 0; c < 26; c++) {
                if (search(root.next[c], word, index + 1)) {
                    isValid = true;
                }
            }
        } else {
            int c = word.charAt(index) - 'a';
            isValid = search(root.next[c], word, index + 1);
        }

        return isValid;

    }
}

// Your WordDictionary object will be instantiated and called as such:
// WordDictionary wordDictionary = new WordDictionary();
// wordDictionary.addWord("word");
// wordDictionary.search("pattern");
```
