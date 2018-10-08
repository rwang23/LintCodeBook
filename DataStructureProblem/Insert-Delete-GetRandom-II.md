##Insert Delete GetRandom O(1) - Duplicates allowed

  Design a data structure that supports all following operations in average O(1) time.

## Example
```
// Init an empty collection.
RandomizedCollection collection = new RandomizedCollection();

// Inserts 1 to the collection. Returns true as the collection did not contain 1.
collection.insert(1);

// Inserts another 1 to the collection. Returns false as the collection contained 1. Collection now contains [1,1].
collection.insert(1);

// Inserts 2 to the collection, returns true. Collection now contains [1,1,2].
collection.insert(2);

// getRandom should return 1 with the probability 2/3, and returns 2 with the probability 1/3.
collection.getRandom();

// Removes 1 from the collection, returns true. Collection now contains [1,2].
collection.remove(1);

// getRandom should return 1 and 2 both equally likely.
collection.getRandom();
Notice
Duplicate elements are allowed.

insert(val): Inserts an item val to the collection.
remove(val): Removes an item val from the collection if present.
getRandom: Returns a random element from current collection of elements. The probability of each element being returned is linearly related to the number of same value the collection contains.
```

###解法

###思路1
- 在I的基础上允许duplicate
- 还是用的I的思想
- 这种题不在乎时间复杂度的其实非常简单,要求O(1)的话,需要对数据结构做一些改变
- 在I的基础上直接做,那么久需要维护一个val -> list of values, 如果只是一个val -> 次数,那么无法找到对应的list中的位置,无法在O(1)进行getRandom
- 最开始想使用HashMap<Integer, List>
- 这样能通过value找到了这个value对应的index list,但是使用List又需要O(k)时间遍历,
- 所以想到了HashMap<Integer, Map<Integer, Integer>>
- value -> a map(list) of nodes, in the map, index -> value
- 这样我们可以通过O(1)完成对这个双重map的操作
- 每次remove的时候都会对这个双重map进行操作,而且都是O(1)

###思路2
- 其实跟思路1差不多
- 变成linkedlist with HashMap 或者 linkedHashMap
- 有head和tail节点进行删除,增加
- [代码](https://www.jiuzhang.com/solution/insert-delete-getrandom-o1-duplicates-allowed/)


```java
class RandomizedCollection {

    /** Initialize your data structure here. */

    // value -> a map(list) of nodes, in the map, index -> value
    Map<Integer, Map<Integer, Integer>> value_map;
    Map<Integer, Integer> index_map;
    List<Integer> list;
    Random rand;

    public RandomizedCollection() {
        value_map = new HashMap<Integer, Map<Integer, Integer>>();
        index_map = new HashMap<Integer, Integer>();
        list = new ArrayList<Integer>();
        rand = new Random();
    }

    /** Inserts a value to the collection. Returns true if the collection did not already contain the specified element. */
    public boolean insert(int val) {
        // write your code here
        Map<Integer, Integer> map = null;
        if (value_map.containsKey(val)) {
            map = value_map.get(val);
        } else {
            map = new HashMap<Integer, Integer>();
        }

        list.add(val);
        map.put(list.size() - 1, val);
        value_map.put(val, map);
        index_map.put(list.size() - 1, val);

        return true;
    }

    /** Removes a value from the collection. Returns true if the collection contained the specified element. */
    public boolean remove(int val) {
        // write your code here
        if (!value_map.containsKey(val)) {
            return false;
        }

        Map<Integer, Integer> map = value_map.get(val);
        if (map.size() == 0) {
            return false;
        }

        Iterator iterator = map.entrySet().iterator();
        Map.Entry pair = (Map.Entry)iterator.next();
        int index = (Integer)pair.getKey();
        map.remove(index);
        index_map.remove(index);

        int last_value = list.get(list.size() - 1);

        if (last_value == val) {
            list.remove(list.size() - 1);
            return true;
        }

        int last_index = list.size() - 1;
        swap(list, index, last_index);
        list.remove(list.size() - 1);

        index_map.remove(last_index);
        index_map.put(index, last_value);

        Map<Integer, Integer> map_of_last = value_map.get(last_value);
        map_of_last.remove(last_index);
        map_of_last.put(index, last_value);

        return true;
    }

    public void swap(List<Integer> list, int index1, int index2) {
        int temp = list.get(index1);
        list.set(index1, list.get(index2));
        list.set(index2, temp);
    }

    /** Get a random element from the collection. */
    public int getRandom() {
        // write your code here
        return list.get(rand.nextInt(list.size()));

    }
}

/**
 * Your RandomizedCollection object will be instantiated and called as such:
 * RandomizedCollection obj = new RandomizedCollection();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```
