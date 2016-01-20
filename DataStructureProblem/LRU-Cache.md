##LRU Cache

18% Accepted

	Design and implement a data structure for Least Recently Used (LRU) cache.
    It should support the following operations: get and set.

	get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
	set(key, value) - Set or insert the value if the key is not already present.
    When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

####Tags Expand
- Linked List

####思路
- 有两种方法：第一种是设置双向链表，第二种是用hashmap储存上一个节点
- 我自己用的单向链表，使用双向链表不太熟悉可能会出现一些问题
- 改造了ListNode listnode当然不仅存next,val,还要存key

####思路

	一定要画图思考 1->2->3->4 (假设数字就是key，capacity大小是4）
	Get
	当get(2)的时候，取出2，怎么达到O(1)去找到2这个节点呢？我们使用了hashmap(key,node)记录下这个节点的位置，所以之后直接通过key找到node，然后就找到节点并使用了。
	但是这里有一点注意的是，如果使用双向链表，我们可以直接找到2的父亲节点从而实现1->3删除掉2，
	但是我们使用单向链表就不行了，回不到父节点。这个时候我们hashmap存的就不是node本身了，而且node的父亲节点，
	所以直接找到了父节点实现1->3，所以这样我们还要使用一个dummy node去指向父节点
	同时1->3还没完成，我们还要重置3的hashmap，因为3的父亲节点变了，我们也要重新put 3的hashmap
	因为使用了2，要重置链表到 1->3->4->2
	put
	如果是1->2->3 要put5, 因为capacity没达到上限，所以直接put 1->2->3->4，直接放在尾节点（所以我们还需要记录尾节点）
	如果1->2->3->4 要put 5，因为capacity达到界限，我们要删除least recently used node，就是1
	2->3->4->5，跟get同理，需要重置2的父亲节点


```java
public class Solution {

    class ListNode {
       int val;
       int key;
       ListNode next;
       ListNode(int val, int key) {
           this.val = val;
           this.key = key;
           this.next = null;
       }
    }

    private HashMap<Integer, ListNode> map;
    private ListNode tail;
    private ListNode dummy;
    private int size;
    private int capacity;

    // @param capacity, an integer
    public Solution(int capacity) {
        // write your code here
        map = new HashMap<Integer, ListNode>();
        dummy = new ListNode(0, 0);
        tail = dummy;
        this.capacity = capacity;
        this.size = 0;
    }

    // @return an integer
    public int get(int key) {
        // write your code here
        if (map.containsKey(key)) {
            ListNode cur = map.get(key);
            ListNode thisCur = cur.next;
            if (cur.next != tail) {
                map.put(cur.next.next.key, cur);
                cur.next = cur.next.next;
                tail.next = thisCur;
                map.put(key, tail);
                tail = tail.next;
                return tail.val;
            } else {
                return tail.val;
            }
        }
        return -1;
    }

    // @param key, an integer
    // @param value, an integer
    // @return nothing
    public void set(int key, int value) {
        // write your code here
        ListNode newNode = new ListNode(value, key);
        if (map.containsKey(key)) {
            ListNode cur = map.get(key);
            if (cur.next != tail) {
                map.put(cur.next.next.key, cur);
                cur.next = cur.next.next;
                tail.next = newNode;
                map.put(key, tail);
                tail = tail.next;
            } else {
                tail.val = value;
                map.put(key, cur);
            }
        } else {
            ListNode prenew = tail;
            tail.next = newNode;
            tail = newNode;
            if (size < capacity) {
                map.put(key, prenew);
                size++;
            } else {
                int deletekey = dummy.next.key;
                map.remove(deletekey);
                dummy = dummy.next;
                map.put(key, prenew);
            }
        }

    }
}

```
