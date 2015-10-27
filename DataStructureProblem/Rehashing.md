##Rehashing

24% Accepted

	The size of the hash table is not determinate at the very beginning.
	If the total size of keys is too large (e.g. size >= capacity / 10),
	we should double the size of the hash table and rehash every keys. Say you have a hash table looks like below:

	size=3, capacity=4

	[null, 21, 14, null]
	       ↓    ↓
	       9   null
	       ↓
	      null
	The hash function is:

	int hashcode(int key, int capacity) {
	    return key % capacity;
	}
	here we have three numbers, 9, 14 and 21, where 21 and 9 share the same position as they all have the same hashcode 1 (21 % 4 = 9 % 4 = 1). We store them in the hash table by linked list.

	rehashing this hash table, double the capacity, you will get:

	size=3, capacity=8

	index:   0    1    2    3     4    5    6   7
	hash : [null, 9, null, null, null, 21, 14, null]
	Given the original hash table, return the new hash table after rehashing .

####Example
	Given [null, 21->9->null, 14->null, null],

	return [null, 9->null, null, null, null, 21->null, 14->null, null]

####Note
 For negative integer in hash table, the position can be calculated as follow:

	C++/Java: if you directly calculate -4 % 3 you will get -1. You can use function: a % b = (a % b + b) % b to make it is a non negative integer.
	Python: you can directly use -1 % 3, you will get 2 automatically.

####Tags Expand
- LintCode Copyright
- Hash Table

####思路

####九章答案
```java
public class Solution {
    /**
     * @param hashTable: A list of The first node of linked list
     * @return: A list of The first node of linked list which have twice size
     */
    public ListNode[] rehashing(ListNode[] hashTable) {
        // write your code here
        if (hashTable.length <= 0) {
            return hashTable;
        }
        int newcapacity = 2 * hashTable.length;
        ListNode[] newTable = new ListNode[newcapacity];
        for (int i = 0; i < hashTable.length; i++) {
            while (hashTable[i] != null) {
                int newindex
                 = (hashTable[i].val % newcapacity + newcapacity) % newcapacity;
                if (newTable[newindex] == null) {
                    newTable[newindex] = new ListNode(hashTable[i].val);
                   // newTable[newindex].next = null;
                } else {
                    ListNode dummy = newTable[newindex];
                    while (dummy.next != null) {
                        dummy = dummy.next;
                    }
                    dummy.next = new ListNode(hashTable[i].val);
                }
                hashTable[i] = hashTable[i].next;
            }
        }
        return newTable;
    }
}
```



####我的解法
- 我的解法并不能在lintcode跑出来，可能题意理解不对，答案是每次把size扩大一倍，然后可能没有实际意义。我的解法是根据实际大小的决定size

```java
/**
 * Definition for ListNode
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
     * @param hashTable: A list of The first node of linked list
     * @return: A list of The first node of linked list which have twice size
     */
    public ListNode[] rehashing(ListNode[] hashTable) {
        // write your code here
        if (hashTable == null) {
            return hashTable;
        }
        Hashtable<Integer, Integer> integerTable = new Hashtable<Integer, Integer>();
        ArrayList<ListNode> listarray = new ArrayList<ListNode>();
        int capacity = hashTable.length;
        for (int i = 0; i < capacity; i++) {
            listarray.add(hashTable[i]);
        }
        boolean breakloop = true;
        while (breakloop) {
            breakloop = false;
            for (int i = 0; i < capacity; i++) {
                ListNode cur = listarray.get(i);
                while(cur != null) {
                    int key;
                    if (cur.val < 0) {
                        key = cur.val % capacity + capacity;
                    } else {
                        key = cur.val % capacity;
                    }
                    if (integerTable.containsKey(key)) {
                        breakloop = true;
                        break;
                    }
                    integerTable.put(key, cur.val);
                    cur = cur.next;
                }
                if (breakloop) {
                    integerTable.clear();
                    break;
                }
            }
            capacity++;
            listarray.add(null);
        }
        ListNode[] result = new ListNode[capacity - 1];
        for (int i = 0; i < capacity - 1; i++) {
            if (integerTable.containsKey(i)) {
                ListNode cur = new ListNode(integerTable.get(i));
                cur.next = null;
                result[i] = cur;
            } else {
                result[i] = null;
            }
        }
        return result;
    }
};


```




