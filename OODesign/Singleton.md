##Singleton

33% Accepted

	Singleton is a most widely used design pattern.
	If a class has and only has one instance at every moment, we call this design as singleton.
	For example, for class Mouse (not a animal mouse), we should design it in singleton.

	You job is to implement a getInstance method for given class, return the same instance of this class every time you call this method.

	Have you met this question in a real interview? Yes
	Example
	In Java:

	A a = A.getInstance();
	A b = A.getInstance();
	a should equal to b.

####Challenge
- If we call getInstance concurrently, can you make sure your code could run correctly?

####Tags Expand
- LintCode Copyright
- OO Design

####思路
- [参考来源](http://www.cnblogs.com/EdwardLiu/p/4443230.html)


####基本解法
- 首先设置s = null, 如果是new一个object的话，很有可能一直不会使用它，就浪费了
- 然后检查是不是建立了instance,所以要判断s==null

```java
class Solution {
    /**
     * @return: The same instance of this class every time
     */
    private static Solution s = null;
    public static Solution getInstance() {
        // write your code here
        if(s == null){
            s = new Solution();
        }
        return s;
    }
};

```

####并发解法
- Suppose there are two threads T1 and T2. Both comes to create instance and execute “instance==null”, now both threads have identified instance variable to null thus assume they must create an instance. They sequentially goes to synchronized block and create the instances. At the end, we have two instances in our application.



```java
class Solution {
    /**
     * @return: The same instance of this class every time
     */
    private static Solution s = null;
    public static Solution getInstance() {
        // write your code here
        if(s == null){
            synchronized (Solution.class) {
                if (s ==null) {
                    s = new Solution();
                }
            }
        }
        return s;
    }
};

```

