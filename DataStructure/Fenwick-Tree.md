##Fenwick Tree / Binary Indexed Tree

[geeksforgeeks](http://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)
[Video](https://www.youtube.com/watch?v=CWDQJGaN1gY)

```java
public class BinaryIndexedTree {

	int[] arr;
	int n;
	BinaryIndexedTree(int[] arr, int n) {
		this.arr = arr;
		this.n = n;
	}

	public int getSum(int[] BITree, int index) {
	    int sum = 0; // Iniialize result

	    // index in BITree[] is 1 more than the index in arr[]
	    index = index + 1;

	    // Traverse ancestors of BITree[index]
	    while (index > 0) {
	        // Add current element of BITree to sum
	        sum += BITree[index];

	        // Move index to parent node in getSum View
	        index -= index & (-index);
	    }
	    return sum;
	}

	// Updates a node in Binary Index Tree (BITree) at given index
	// in BITree.  The given value 'val' is added to BITree[i] and
	// all of its ancestors in tree.
	public void updateBIT(int[] BITree, int n, int index, int val) {
	    // index in BITree[] is 1 more than the index in arr[]
	    index = index + 1;

	    // Traverse all ancestors and add 'val'
	    while (index <= n) {
	       // Add 'val' to current node of BI Tree
	       BITree[index] += val;

	       // Update index to that of parent in update View
	       index += index & (-index);
	    }
	}

	// Constructs and returns a Binary Indexed Tree for given
	// array of size n.
	public int constructBITree(int[] arr, int n) {
	    // Create and initialize BITree[] as 0
	    int[] BITree = new int[n+1];
	    for (int i=1; i<=n; i++) {
	        BITree[i] = 0;
	    }
	    // Store the actual values in BITree[] using update()
	    for (int i=0; i<n; i++) {
	        updateBIT(BITree, n, i, arr[i]);
	    }
	    // Uncomment below lines to see contents of BITree[]
	    //for (int i=1; i<=n; i++) {
	    //      System.out.println(BITree[i]);
	    //}

	    return BITree;
	}
}

```
