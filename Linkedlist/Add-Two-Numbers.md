##Add Two Numbers

21% Accepted

	You have two numbers represented by a linked list, where each node contains a single digit.
    The digits are stored in reverse order, such that the 1's digit is at the head of the list.
    Write a function that adds the two numbers and returns the sum as a linked list.

	Have you met this question in a real interview? Yes
	Example
	Given 7->1->6 + 5->9->2. That is, 617 + 295.

	Return 2->1->9. That is 912.

	Given 3->1->5 and 5->9->2, return 8->0->8.

####Tags Expand
- Cracking The Coding Interview
- Linked List
- High Precision



####解法一
- 使用了StringBuffer去解决问题，去避免了Linkedlist太长，导致int或者long溢出的问题
- Lintcode跑完所有case是1100ms左右
- Character.getNumericValue(res.charAt(i)) 将char转化为int
- 创建了string add 函数，以后可以自己调用

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param l1: the first list
     * @param l2: the second list
     * @return: the sum list of l1 and l2
     */
    public ListNode addLists(ListNode l1, ListNode l2) {
        // write your code here
        if (l1 == null || l2 == null) {
            return null;
        }
        StringBuffer res = stringadd(getnum(l1), getnum(l2));
        int len = res.length();
        ListNode root = new ListNode(0);
        ListNode cur = root;
        for (int i = len - 1; i >= 0; i--) {
            cur.val = Character.getNumericValue(res.charAt(i));
            if (i != 0) {
                ListNode next = new ListNode(0);
                cur.next = next;
                cur = cur.next;
            }
        }
        return root;

    }
    public StringBuffer getnum(ListNode l1) {
        StringBuffer sum = new StringBuffer("");
        sum.append(l1.val);
        while (l1.next != null) {
            sum.insert(0,l1.next.val);
            l1 = l1.next;
        }
        return sum;
    }

    public StringBuffer stringadd(StringBuffer s1, StringBuffer s2) {
        int len1 = s1.length();
        int len2 = s2.length();
        int i = 0;
        StringBuffer res = new StringBuffer("");
        int carry = 0;
        while (i < Math.max(len1, len2)) {

            int add1, add2;
            if (i < len1) {
                add1 = Character.getNumericValue(s1.charAt(len1 - 1 - i));
            } else {
                add1 = 0;
            }
            if (i < len2) {
                add2 = Character.getNumericValue(s2.charAt(len2 - 1 - i));
            } else {
                add2 = 0;
            }
            int sum = (add1 + add2 + carry) % 10;
            if ((add1 + add2 + carry) >= 10) {
                carry = 1;
            } else {
                carry = 0;
            }
            i++;
            res.insert(0, sum);
        }
        if (carry == 1) {
            res.insert(0, 1);
        }
        return res;
    }
}

```


####解法二
- 来自九章
- 时间也在1200ms左右
- 直接计算，根本不必要去读取linkedlist数值，因为本来就翻转的，最前面的数就是个位数，其次是十位数，直接相加就可以了

```java
public class Solution {
    public ListNode addLists(ListNode l1, ListNode l2) {
        if(l1 == null && l2 == null) {
            return null;
        }

        ListNode head = new ListNode(0);
        ListNode point = head;
        int carry = 0;
        while(l1 != null && l2!=null){
            int sum = carry + l1.val + l2.val;
            point.next = new ListNode(sum % 10);
            carry = sum / 10;
            l1 = l1.next;
            l2 = l2.next;
            point = point.next;
        }

        while(l1 != null) {
            int sum =  carry + l1.val;
            point.next = new ListNode(sum % 10);
            carry = sum /10;
            l1 = l1.next;
            point = point.next;
        }

        while(l2 != null) {
            int sum =  carry + l2.val;
            point.next = new ListNode(sum % 10);
            carry = sum /10;
            l2 = l2.next;
            point = point.next;
        }

        if (carry != 0) {
            point.next = new ListNode(carry);
        }
        return head.next;
    }
}
```
