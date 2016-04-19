##Implement Trie (Prefix Tree)
	Total Accepted: 34060 Total Submissions: 134340 Difficulty: Medium
	Implement a trie with insert, search, and startsWith methods.

	Note:
	You may assume that all inputs are consist of lowercase letters a-z.

####思路

```java
class TrieNode {
    // Initialize your data structure here.
    int value;
    TrieNode[] next = new TrieNode[26];
    public TrieNode() {
    }
}

public class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    // Inserts a word into the trie.
    public void insert(String word) {
        insert(word, 1, 0, root);
    }

    public TrieNode insert(String word, int val, int index, TrieNode root) {
        if (root == null) {
            root = new TrieNode();
        }

        if (index == word.length()) {
            root.value = val;
            return root;
        }

        int c = word.charAt(index) - 'a';
        root.next[c] = insert(word, val, index + 1, root.next[c]);

        return root;
    }

    // Returns if the word is in the trie.
    public boolean search(String word) {
        return search(word, root, 0) != 0;
    }

    public int search(String word, TrieNode root, int index) {
        if (root == null) {
            return 0;
        }

        if (index == word.length()) {
            if (root.value != 0) {
                return root.value;
            } else {
                return 0;
            }
        }

        int c = word.charAt(index) - 'a';
        return search(word, root.next[c], index + 1);
    }

    // Returns if there is any word in the trie
    // that starts with the given prefix.
    public boolean startsWith(String prefix) {
        return startsWith(prefix, root, 0);
    }

    public boolean startsWith(String prefix, TrieNode root, int index) {
        if (root == null) {
            return false;
        }

        if (index == prefix.length()) {
            if (root != null) {
                return true;
            } else {
                return false;
            }
        }

        int c = prefix.charAt(index) - 'a';
        return startsWith(prefix, root.next[c], index + 1);
    }
}

// Your Trie object will be instantiated and called as such:
// Trie trie = new Trie();
// trie.insert("somestring");
// trie.search("key");
```
