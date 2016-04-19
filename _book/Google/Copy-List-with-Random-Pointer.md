##Copy List with Random Pointer

27% Accepted

	A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

	Return a deep copy of the list.



####Challenge
Could you solve it with O(1) space?

####Tags Expand
- Hash Table
- Linked List

####思路
- 第一种思路是创建一个正常链表，用hashmap来存储随机结点，但是这样空间是O(n)
- 第二种思路是对链表进行三次扫描
- 第一次扫描对每个结点进行复制，链表的下一个值是自己的复制，然后是下一个值
- 1->2->3->4->5->6变成 1->1->2->2->3->3->4->4->5->5->6->6
- 第二次扫描中我们把旧结点的随机指针赋给新节点的随机指针， 因为新结点都跟在旧结点的下一个值得注意的是，要赋值到新节点的随机值，node.random.next，其中node.next就是新结点
- 最后将链表拆开，跳着赋值拆开就可以了

####方法一
```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    /**
     * @param head: The head of linked list with a random pointer.
     * @return: A new head of a deep copy of the list.
     */
    public RandomListNode copyRandomList(RandomListNode head) {
        // write your code here
        if (head == null) {
            return head;
        }

        HashMap<RandomListNode, RandomListNode> hashmap = new HashMap<RandomListNode, RandomListNode>();
        RandomListNode dummy = new RandomListNode(0);
        dummy.next = head;

        RandomListNode newdummy = new RandomListNode(0);
        RandomListNode newNode = newdummy;

        while (head != null) {
            RandomListNode copy = new RandomListNode(head.label);
            newNode.next = copy;
            hashmap.put(head, copy);
            newNode = newNode.next;
            head = head.next;
        }

        newNode = newdummy.next;
        head = dummy.next;

        while (head != null) {
            RandomListNode randomnode = hashmap.get(head.random);
            newNode.random = randomnode;
            head = head.next;
            newNode = newNode.next;
        }
        return newdummy.next;
    }
}
```

####方法二
```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    /**
     * @param head: The head of linked list with a random pointer.
     * @return: A new head of a deep copy of the list.
     */
    public RandomListNode copyRandomList(RandomListNode head) {
        // write your code here
        if (head == null) {
            return head;
        }

        RandomListNode dummy = new RandomListNode(0);
        dummy.next = head;

        while (head != null) {
            RandomListNode newNode = new RandomListNode(head.label);
            RandomListNode next = head.next;
            head.next = newNode;
            newNode.next = next;
            head = next;
        }

        head = dummy.next;
        while (head != null) {
            RandomListNode random = head.random;
            if (random != null) {
                head.next.random = random.next;
            }
            head = head.next.next;
        }

        RandomListNode pre = dummy;
        head = dummy.next;
        while (head != null) {
            RandomListNode next = head.next;
            pre.next = next;
            head = head.next.next;
            pre = next;
        }

        return dummy.next;
    }
}
```
