##Insert Delete GetRandom O(1)

  Design a data structure that supports all following operations in average O(1) time.

  insert(val): Inserts an item val to the set if not already present.
  remove(val): Removes an item val from the set if present.
  getRandom: Returns a random element from current set of elements. Each element must have the same probability of being returned.

##Example
```java
// Init an empty set.
RandomizedSet randomSet = new RandomizedSet();

// Inserts 1 to the set. Returns true as 1 was inserted successfully.
randomSet.insert(1);

// Returns false as 2 does not exist in the set.
randomSet.remove(2);

// Inserts 2 to the set, returns true. Set now contains [1,2].
randomSet.insert(2);

// getRandom should return either 1 or 2 randomly.
randomSet.getRandom();

// Removes 1 from the set, returns true. Set now contains [2].
randomSet.remove(1);

// 2 was already in the set, so return false.
randomSet.insert(2);

// Since 2 is the only number in the set, getRandom always return 2.
randomSet.getRandom();
```

###解法
- 本来想自己在写个ListNode,但是根本不必要
- 又不需要记录顺序,并不需要ListNode
- 需要random那么需要index去获得,那么最后只需要一个数列和hashmap就行了

```java
public class RandomizedSet {

    ArrayList<Integer> nums;
    HashMap<Integer, Integer> num2index;
    Random rand;

    public RandomizedSet() {
        // do initialize if necessary
        nums = new ArrayList<Integer>();
        num2index = new HashMap<Integer, Integer>();  
        rand = new Random();
    }

    // Inserts a value to the set
    // Returns true if the set did not already contain the specified element or false
    public boolean insert(int val) {
        if (num2index.containsKey(val)) {
            return false;
        }

        num2index.put(val, nums.size());
        nums.add(val);
        return true;
    }

    // Removes a value from the set
    // Return true if the set contained the specified element or false
    public boolean remove(int val) {
        if (!num2index.containsKey(val)) {
            return false;
        }

        int index = num2index.get(val);
        if (index < nums.size() - 1) { // not the last one than swap the last one with this val
            int last = nums.get(nums.size() - 1);
            nums.set(index, last);
            num2index.put(last, index);
        }
        num2index.remove(val);
        nums.remove(nums.size() - 1);
        return true;
    }

    // Get a random element from the set
    public int getRandom() {
        return nums.get(rand.nextInt(nums.size()));
    }
}

```
