##Word Search II

	Total Accepted: 16969 Total Submissions: 90342 Difficulty: Hard
	Given a 2D board and a list of words from the dictionary, find all words in the board.

	Each word must be constructed from letters of sequentially adjacent cell,
    where "adjacent" cells are those horizontally or vertically neighboring.
    The same letter cell may not be used more than once in a word.

	For example,
	Given words = ["oath","pea","eat","rain"] and board =

	[
	  ['o','a','a','n'],
	  ['e','t','a','e'],
	  ['i','h','k','r'],
	  ['i','f','l','v']
	]
	Return ["eat","oath"].
	Note:
	You may assume that all inputs are consist of lowercase letters a-z.

####思路
- Trie + DFS
- 22分钟写完,但是debug花了四十分钟(四十分钟debug跑过了自己的test case, 又用了二十分钟过了lintcode test case,再用了五分钟过了leetcode test case)
- bug存在于很小的细节(写了两个newX,没写newY,debug半小时)
- Trie没有必要fully implement,只需要先有了add(put)功能,之后的根据需要再写
- 构造Trie的时候,构造了parent指针,这样方便回溯
- 代码写了main函数来测试

####Leetcode
```java
import java.util.ArrayList;
import java.util.List;

public class Solution {

    class TrieNode{
        TrieNode[] next;
        TrieNode parent;
        int value;
        TrieNode() {
            next = new TrieNode[26];
            parent = null;
            int value = 0;
        }
    }

    private class Trie{
        private TrieNode root = new TrieNode();

        public void put(String s) {
            put(root, s, 0, 1);
        }

        public TrieNode put(TrieNode root, String s, int index, int value) {
            if (root == null) {
                root = new TrieNode();
            }

            if (index == s.length()) {
                root.value = value;
                return root;
            }

            int c = s.charAt(index) - 'a';
            root.next[c] = put(root.next[c], s, index + 1, value);
            root.next[c].parent = root;
            return root;
        }

        private TrieNode searchNode = root;
        public boolean isValid(char c) {
            if (searchNode == null) {
                return false;
            }
            int x = c - 'a';
            return searchNode.next[x] != null;
        }
    }

    public List<String> findWords(char[][] board, String[] words) {
        List<String> result = new ArrayList<String>();
        if (board.length == 0 || board[0].length == 0 || words.length == 0) {
            return result;
        }

        int m = board.length;
        int n = board[0].length;

        Trie myTrie = new Trie();
        for (int i = 0; i < words.length; i++) {
            myTrie.put(words[i]);
        }

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int[][] visited = new int[m][n];
                StringBuilder s = new StringBuilder();
                dfs(result, myTrie, i, j, board, s, visited);
            }
        }

        return result;
    }

    public void dfs(List<String> result, Trie myTrie, int x, int y, char[][] board, StringBuilder s, int[][] visited) {

        if (myTrie.searchNode.value != 0 && !result.contains(s.toString())) {
            result.add(new String(s));
        }

        if (myTrie.searchNode == null) {
            return;
        }

        if (!(x < board.length && y < board[0].length && x >= 0 && y >= 0 && visited[x][y] == 0)) {
            return;
        }

        char c = board[x][y];

        int[] xStep = new int[]{0,  0, 1, -1};
        int[] yStep = new int[]{1, -1, 0,  0};

        if (myTrie.isValid(c)) {
            for (int i = 0; i < 4; i++) {
                int newX = x + xStep[i];
                int newY = y + yStep[i];
                char myChar = board[x][y];
                s.append(myChar);
                visited[x][y] = 1;
                myTrie.searchNode = myTrie.searchNode.next[c - 'a'];
                dfs(result, myTrie, newX, newY, board, s, visited);
                s.deleteCharAt(s.length() - 1);
                visited[x][y] = 0;
                myTrie.searchNode = myTrie.searchNode.parent;
            }
        } else {
            return;
        }
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        char[][] board = new char[][]{{'a','b','c','e'},{'s','f','c','s'},{'a','d','e','e'}};
        String[] string = new String[]{"abcb", "ninechapter", "lintcode"};
        List<String> result = sol.findWords(board, string);
        for(String s: result) {
            System.out.println(s);
        }
        System.out.println("It is done");

    }
}
```


####Lintcode

```java
public class Solution {
    /**
     * @param board: A list of lists of character
     * @param words: A list of string
     * @return: A list of string
     */
    class TrieNode{
        TrieNode[] next;
        TrieNode parent;
        int value;
        TrieNode() {
            next = new TrieNode[26];
            parent = null;
            int value = 0;
        }
    }

    private class Trie{
        private TrieNode root = new TrieNode();

        public void put(String s) {
            put(root, s, 0, 1);
        }

        public TrieNode put(TrieNode root, String s, int index, int value) {
            if (root == null) {
                root = new TrieNode();
            }

            if (index == s.length()) {
                root.value = value;
                return root;
            }

            int c = s.charAt(index) - 'a';
            root.next[c] = put(root.next[c], s, index + 1, value);
            root.next[c].parent = root;
            return root;
        }

        private TrieNode searchNode = root;
        public boolean isValid(char c) {
            if (searchNode == null) {
                return false;
            }
            int x = c - 'a';
            return searchNode.next[x] != null;
        }
    } 
     
    public List<String> wordSearchII(char[][] board, List<String> words) {
        // write your code here
        List<String> result = new ArrayList<String>();
        if (board.length == 0 || board[0].length == 0 || words.size() == 0) {
            return result;
        }

        int m = board.length;
        int n = board[0].length;

        Trie myTrie = new Trie();
        for (int i = 0; i < words.size(); i++) {
            myTrie.put(words.get(i));
        }

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int[][] visited = new int[m][n];
                StringBuilder s = new StringBuilder();
                dfs(result, myTrie, i, j, board, s, visited);
            }
        }

        return result;
    }

    public void dfs(List<String> result, Trie myTrie, int x, int y, char[][] board, StringBuilder s, int[][] visited) {

        if (myTrie.searchNode.value != 0 && !result.contains(s.toString())) {
            result.add(new String(s));
        }

        if (myTrie.searchNode == null) {
            return;
        }

        if (!(x < board.length && y < board[0].length && x >= 0 && y >= 0 && visited[x][y] == 0)) {
            return;
        }

        char c = board[x][y];

        int[] xStep = new int[]{0,  0, 1, -1};
        int[] yStep = new int[]{1, -1, 0,  0};

        if (myTrie.isValid(c)) {
            for (int i = 0; i < 4; i++) {
                int newX = x + xStep[i];
                int newY = y + yStep[i];
                char myChar = board[x][y];
                s.append(myChar);
                visited[x][y] = 1;
                myTrie.searchNode = myTrie.searchNode.next[c - 'a'];
                dfs(result, myTrie, newX, newY, board, s, visited);
                s.deleteCharAt(s.length() - 1);
                visited[x][y] = 0;
                myTrie.searchNode = myTrie.searchNode.parent;
            }
        } else {
            return;
        }
    }
}
```
