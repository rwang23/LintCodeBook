##Delete Node in the Middle of Singly Linked List

37% Accepted

	Implement an algorithm to delete a node in the middle of a singly linked list, given only access to that node.

	Have you met this question in a real interview? Yes
	Example
	Given 1->2->3->4, and node 3. return 1->2->4

####Tags Expand
- Cracking The Coding Interview
- Linked List

####思路
- 一来就想找前面节点，是无法实现的
- 可以通过复制后面的节点到前面来，就可以实现了

```java
public class Solution {
    /**
     * @param node: the node in the list should be deleted
     * @return: nothing
     */
    public void deleteNode(ListNode node) {
        // write your code here
        ListNode temp = node.next;
        node.val = temp.val;
        node.next = temp.next;
    }
}

```
