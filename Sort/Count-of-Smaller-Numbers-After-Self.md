##Count of Smaller Numbers After Self

	Total Accepted: 6186 Total Submissions: 21480 Difficulty: Hard
	You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].

	Example:

	Given nums = [5, 2, 6, 1]

	To the right of 5 there are 2 smaller elements (2 and 1).
	To the right of 2 there is only 1 smaller element (1).
	To the right of 6 there is 1 smaller element (1).
	To the right of 1 there is 0 smaller element.
	Return the array [2, 1, 1, 0].

####思路
- O(n2) 暴力解法

```java
public class Solution {
    public List<Integer> countSmaller(int[] nums) {
        int n = nums.length;
        List<Integer> result = new ArrayList<Integer>();

        if (n == 0) {
            return result;
        }

        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                if (nums[j] < nums[i]) {
                    result.add(nums[j]);
                }
            }
        }
        return result;
    }
}
```

####优化解法
- 使用逆序数有经典的解法为合并排序 O(nlogn)
- 设置了一个Node class来进行合并排序,(当然也不需要这个class,设置好index, count数组也可以,但是更难理解)
- 使用stable sort,在交换的时候,因为左边比右边大才会进行交换,所以对左边的这个Node的count++
- 同时,因为在mid前边,这个Node后边的所有Node都需要进行count++,这里使用了一个smaller寄存器来储存,在需要使用这个点的时候,在count + smaller

```java
public class Solution {
    private class Node {
        private int value;
        private int count;
        private int index;
        Node (int value, int index, int count) {
            this.value = value;
            this.index = index;
            this.count = count;
        }
    }
    public List<Integer> countSmaller(int[] nums) {
        List<Integer> result = new ArrayList<Integer>();
        if (nums == null || nums.length == 0) {
            return result;
        }

        int size = nums.length;
        Node[] nodes = new Node[size];
        for (int i = 0; i < size; i++) {
            nodes[i] = new Node(nums[i], i, 0);
        }
        Node[] aux = new Node[size];
        sort(nodes, aux, 0, size - 1);

        Arrays.sort(nodes, new Comparator<Node>() {
            public int compare(Node n1, Node n2) {
                return n1.index - n2.index;
            }
        });
        for (int i = 0; i < size; i++) {
            result.add(nodes[i].count);
        }

        return result;
    }

    public void sort(Node[] nodes, Node[] aux, int lo, int hi) {
        if (lo >= hi) {
            return;
        }

        int mid = lo + (hi - lo) / 2;
        sort(nodes, aux, lo, mid);
        sort(nodes, aux, mid + 1, hi);
        merge(nodes, aux, lo, mid, hi);
    }

    public void merge (Node[] nodes, Node[] aux, int lo, int mid, int hi) {

        for (int i = lo; i <= hi; i++) {
            aux[i] = new Node(nodes[i].value, nodes[i].index, nodes[i].count);
        }
        int start = lo;
        int end = mid + 1;
        int smaller = 0;

        for (int i = lo; i <= hi; i++) {

            if (start > mid) {
                Node cur = aux[end++];
                nodes[i] = new Node(cur.value, cur.index, cur.count);
            } else if (end > hi) {
                Node cur = aux[start++];
                nodes[i] = new Node(cur.value, cur.index, cur.count);
                nodes[i].count += smaller;

            } else if (aux[end].value >= aux[start].value) {
                Node cur = aux[start++];
                nodes[i] = new Node(cur.value, cur.index, cur.count);
                nodes[i].count += smaller;
            } else {
                Node cur = aux[end++];
                nodes[i] = new Node(cur.value, cur.index, cur.count);
                smaller++;
            }
        }
    }
}
```

####此题还可以使用线段树,binary indexed tree, BST
- [参考](https://leetcode.com/discuss/73762/9ms-short-java-bst-solution-get-answer-when-building-bst)

```
    Every node will maintain a val sum recording the total of number on it's left bottom side,
    dup counts the duplication.
    For example, [3, 2, 2, 6, 1], from back to beginning,we would have:

                    1(0, 1)
                         \
                         6(3, 1)
                         /
                       2(0, 2)
                           \
                            3(0, 1)
    When we try to insert a number,
    the total number of smaller number would be adding dup and sum of the nodes
    where we turn right.
    for example, if we insert 5, it should be inserted on the way down to the right of 3, the nodes
    where we turn right is 1(0,1), 2,(0,2), 3(0,1),
    so the answer should be (0 + 1)+(0 + 2)+ (0 + 1) = 4

    if we insert 7, the right-turning nodes are 1(0,1), 6(3,1),
    so answer should be (0 + 1) + (3 + 1) = 5
```


```java
public class Solution {
    class Node {
        Node left, right;
        int val, sum, dup = 1;
        public Node(int v, int s) {
            val = v;
            sum = s;
        }
    }
    public List<Integer> countSmaller(int[] nums) {
        Integer[] ans = new Integer[nums.length];
        Node root = null;
        for (int i = nums.length - 1; i >= 0; i--) {
            root = insert(nums[i], root, ans, i, 0);
        }
        return Arrays.asList(ans);
    }
    private Node insert(int num, Node node, Integer[] ans, int i, int preSum) {
        if (node == null) {
            node = new Node(num, 0);
            ans[i] = preSum;
        } else if (node.val == num) {
            node.dup++;
            ans[i] = preSum + node.sum;
        } else if (node.val > num) {
            node.sum++;
            node.left = insert(num, node.left, ans, i, preSum);
        } else {
            node.right = insert(num, node.right, ans, i, preSum + node.dup + node.sum);
        }
        return node;
    }
}
```
