##k Sum II

32% Accepted

	Given n unique integers, number k (1<=k<=n)  and target.
	Find all possible k integers where their sum is target.

	Have you met this question in a real interview? Yes
	Example
	Given [1,2,3,4], k=2, target=5, [1,4] and [2,3] are possible solutions.

####Tags Expand
- LintCode Copyright
- Depth First Search

####思路
- k sum I的变形题，但是简单很多，就是DFS，K sum也可以用DFS但是要超时
- 标准DFS


```java
public class Solution {
    /**
     * @param A: an integer array.
     * @param k: a positive integer (k <= length(A))
     * @param target: a integer
     * @return a list of lists of integer
     */
    public ArrayList<ArrayList<Integer>> kSumII(int A[], int k, int target) {
        // write your code here
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
        ArrayList<Integer> combination = new ArrayList<Integer>();
        dfs(A, result, combination, target, k, 0, 0);
        return result;

    }

    public void dfs(int[] A, ArrayList<ArrayList<Integer>> result, ArrayList<Integer> combination, int target, int k, int pos, int sum) {
        if (combination.size() == k && sum == target) {
            result.add(new ArrayList<Integer>(combination));
        } else if (combination.size() > k || sum > target) {
            return;
        }

        for (int i = pos; i < A.length; i++) {
            combination.add(A[i]);
            sum += A[i];
            dfs(A, result, combination, target, k, i + 1 , sum);
            sum -= A[i];
            combination.remove(combination.size() - 1);
        }
    }
}


```
