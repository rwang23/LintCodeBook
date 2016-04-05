##Find the Celebrity

	Total Accepted: 6806 Total Submissions: 19473 Difficulty: Medium

	Suppose you are at a party with n people (labeled from 0 to n - 1) and among them, there may exist one celebrity.
	The definition of a celebrity is that all the other n - 1 people know him/her but he/she does not know any of them.

	Now you want to find out who the celebrity is or verify that there is not one.
	The only thing you are allowed to do is to ask questions like: "Hi, A. Do you know B?"
	to get information of whether A knows B.
	You need to find out the celebrity (or verify there is not one) by asking as few questions as possible (in the asymptotic sense).

	You are given a helper function bool knows(a, b) which tells you whether A knows B.
	Implement a function int findCelebrity(n), your function should minimize the number of calls to knows.

	Note: There will be exactly one celebrity if he/she is in the party.
	Return the celebrity's label if there is a celebrity in the party. If there is no celebrity, return -1.

####思路
- using stack
- [geeksforgeeks](http://www.geeksforgeeks.org/the-celebrity-problem/)

```
The graph construction takes O(N2) time, it is similar to brute force search. In case of recursion, we reduce the problem instance by not more than one, and also combine step may examine M-1 persons (M – instance size).

We have following observation based on elimination technique (Refer Polya’s How to Solve It book).

If A knows B, then A can’t be celebrity. Discard A, and B may be celebrity.
If A doesn’t know B, then B can’t be celebrity. Discard B, and A may be celebrity.
Repeat above two steps till we left with only one person.
Ensure the remained person is celebrity. (Why do we need this step?)
We can use stack to verity celebrity.

Push all the celebrities into a stack.
Pop off top two persons from the stack, discard one person based on return status of HaveAcquaintance(A, B).
Push the remained person onto stack.
Repeat step 2 and 3 until only one person remains in the stack.
Check the remained person in stack doesn’t have acquaintance with anyone else.
```

```java
/* The knows API is defined in the parent class Relation.
      boolean knows(int a, int b); */

public class Solution extends Relation {
    public int findCelebrity(int n) {
        if (n <= 1) {
            return -1;
        }

        Stack<Integer> stack = new Stack<Integer>();
        for (int i = 0; i < n; i++) {
            stack.push(i);
        }

        while (stack.size() != 1) {
            int person1 = stack.pop();
            int person2 = stack.pop();
            if (knows(person1, person2)) {
                stack.push(person2);
            } else {
                stack.push(person1);
            }
        }

        int candidate = stack.pop();

        for (int i = 0; i < n; i++) {
            if (i == candidate) {
                continue;
            }
            if (knows(candidate, i)) {
                return -1;
            }
            if (!knows(i, candidate)) {
                return -1;
            }
        }

        return candidate;
    }
}
```
