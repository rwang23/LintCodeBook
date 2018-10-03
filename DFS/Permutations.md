##Permutations

	Given a list of numbers, return all possible permutations.

	For nums = [1,2,3], the permutations are:

	[
	  [1,2,3],
	  [1,3,2],
	  [2,1,3],
	  [2,3,1],
	  [3,1,2],
	  [3,2,1]
	]

####Challenge
- Do it without recursion.

####Tags: Recursion

####递归思路
- 三个数取一次
- 就算先取了2，也必须回过去找1，所以可以用不设限制条件的循环，重新去找1
- 如果又遇到了2，跳过就可以


```java
public class Solution {
    /*
     * @param nums: A list of integers.
     * @return: A list of permutations.
     */
    public List<List<Integer>> permute(int[] nums) {
        // write your code here
        List<List<Integer>> results = new ArrayList<List<Integer>>();
        
        if (nums == null || nums.length == 0) {
            results.add(new ArrayList<Integer>());
            return results;
        }
        
        boolean[] visited = new boolean[nums.length];
        List<Integer> list = new ArrayList<Integer>();
        
        dfs(results, list, nums, visited);
        
        return results;
        
    }
    
    public void dfs(List<List<Integer>> results, List<Integer> list, int[] nums, boolean[] visited) {
        
        if (list.size() == nums.length) {
            List<Integer> target = new ArrayList<Integer>(list);
            results.add(target);
            return;
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (visited[i]) {
                continue;
            }
            
            list.add(nums[i]);
            visited[i] = true;
            dfs(results, list, nums, visited);
            visited[i] = false;
            list.remove(list.size() - 1);
        }
    }
}
```

###非递归思路1
- next permutation的思路
- 全排列就是从第一个数字起每个数分别与它后面的数字交换
- 去重的全排列就是从第一个数字起每个数分别与它后面非重复出现的数字交换
- 全排列的非递归就是由后向前找替换数和替换点，然后由后向前找第一个比替换数大的数与替换数交换，最后颠倒替换点后的所有数据。

```
permutation iterative固定做法
从后往前寻找索引满足 a[k] < a[k + 1], 如果此条件不满足，则说明已遍历到最后一个。
从后往前遍历，找到第一个比a[k]大的数a[l], 即a[k] < a[l].
交换a[k]与a[l].
反转k + 1 ~ n之间的元素。
input [1,3,2]
第一步,发现1 < 3 所以 i 指向的是1这个元素 = 0
第二步,从后面往前找第一个比1大的数,发现是2,index是2
第三步,交换a[0] a[2] 数组变成[2,3,1]
第四步, 翻转i+1 到最后 数组变成[2,1,3]
得到答案
```

```java
public class Solution {
    /*
     * @param nums: A list of integers.
     * @return: A list of permutations.
     */
    public List<List<Integer>> permute(int[] nums) {
        // write your code here
        List<List<Integer>> results = new ArrayList<List<Integer>>();

        if (nums == null || nums.length == 0) {
            results.add(new ArrayList<Integer>());
            return results;
        }
        
        Arrays.sort(nums);
        results.add(toList(nums));
        
        while (true) {
            int target = -1;
            for (int k = nums.length - 2; k >= 0; k--) {
                if (nums[k] < nums[k + 1]) {
                    target = k;
                    break;
                }
            }
            
            if (target == -1) {
                break;
            }
            
            for (int j = nums.length - 1; j >= target + 1; j--) {
                if (nums[j] > nums[target]) {
                    swap(target, j, nums);
                    break;
                }
            }
            
            reverse(target + 1, nums.length - 1, nums);
            
            
            List<Integer> list = toList(nums);
            results.add(list);
        }
        
        return results;
    }
    
    public void reverse(int start, int end, int[] nums) {
        for (int i = start, j = end; i < j; i++,j--) {
            int temp = nums[i];
            nums[i] = nums[j];
            nums[j] = temp;
        }
    }
    
    public void swap(int start, int end, int[] nums) {
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
    }
    
    public List<Integer> toList(int[] nums) {
        List<Integer> list = new ArrayList<Integer>();
        for (int i : nums) {
            list.add(i);
        }
        return list;
    }
}
```

###非递归思路2
- [参考](https://blog.csdn.net/happyaaaaaaaaaaa/article/details/51534048)
- 假设我们有了当前前 i 个元素的组合，当第 i+1个元素加入时，我们需要做的是将这个元素加入之前的每一个结果，并且放在每个结果的每个位置，因为之前的结果没有重复，所以加入新元素的结果也不会有重复（这里是假定数字集合没有重复）

####使用queue，更好理解
```
public class Solution {
    /*
     * @param nums: A list of integers.
     * @return: A list of permutations.
     */
    public List<List<Integer>> permute(int[] nums) {
        // write your code here
        List<List<Integer>> results = new ArrayList<List<Integer>>();
        List<Integer> list = new ArrayList<Integer>();
        Queue<List<Integer>> queue = new LinkedList<List<Integer>>();
        
        if (nums == null || nums.length == 0) {
            results.add(new ArrayList<Integer>());
            return results;
        }
        
	//单独处理只有一个元素的时候
        if (nums.length == 1) {
            list.add(nums[0]);
            results.add(list);
            return results;
        }
      
        list.add(nums[0]);
        queue.offer(list);
        int index = 1;
        
        while (!queue.isEmpty()) {
	    //层级BFS遍历，每次进入下一层，再把下一个数加进来
            int queueSize = queue.size();
            for (int i = 0; i < queueSize; i++) {
                List<Integer> cur = queue.poll();
                int insert = nums[index];
                int size = cur.size();
                for (int j = 0; j <= size; j++) {
                    List<Integer> addList = new ArrayList<Integer>(cur);
                    addList.add(j, insert);
                    if (addList.size() == nums.length) {
                        results.add(addList);
                    } else {
                        queue.offer(addList);
                    }
                }
            }
            index++;
        }
        
        return results;
    }
}
```
####使用list

```java
public class Solution {
     public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> first = new ArrayList<>();
        first.add(nums[0]);
        res.add(first);
        for(int i = 1; i < nums.length; i++) {
            List<List<Integer>> newRes = new ArrayList<>();
            for(List<Integer> temp : res) {
                int size = temp.size() + 1;
                for(int j = 0; j < size; j++) {
                    List<Integer> item = new ArrayList<>(temp);
                    item.add(j, nums[i]);
                    newRes.add(item);
                }
            }
            res = newRes;
        }
        return res;
    }
}
```
