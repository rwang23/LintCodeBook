###Some Common Use

####If string is null, we cannot use string.length()

####Java Timing
	long startTime = System.nanoTime();
	function performed
	long endTime = System.nanoTime();
	long totalTime = (endTime - startTime) / 1000000000.0;
	System.out.println(totalTime);

####Charater to Integer
	Character.getNumericValue(c)
	It returns -1 if the character is not a digit.
	int result = c - '0'
####is Character a integer
      System.out.println(Character.isDigit('c'));
      System.out.println(Character.isDigit('5'));

####Integer to Character
	int a = 1;
	char b = (char)(a + '0');

####Integer to String
Integer.toString(number)
String.valueOf(number)

####String to Integer
	int foo = Integer.parseInt("1234");
	(If you have it in a StringBuffer, you'll need to do Integer.parseInt(myBuffer.toString()); instead).
	Integer x = Integer.valueOf(str);

####String[] arrays 转化成string
Arrays.toString();

####Character.toLowerCase()
####Character.toUpperCase()
####Arrays Binary Search
Arrays.binarySearch(dp, 0, len, nums[i])
####sort reverse order
	对于array与arraylist
	Arrays.sort(arraylist, Collections.reverseOrder());
	Collections.sort(arraylist, Collections.reverseOrder());

####arrays to arraylist
```java
public class ArrayDemo1 {
   public static void main (String args[]) {

   // create an array of strings
   String a[] = new String[]{"abc","klm","xyz","pqr"};

   List list1 = Arrays.asList(a);

   // printing the list
   System.out.println("The list is:" + list1);
   }
}


The list is:[abc, klm, xyz, pqr]
```
####Copy array
```java
    int[] a = {1,2,3};
    int[] b = Arrays.copyOfRange(a, 0, a.length);
```

####array 初始化
```java
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
```

####使用二进制运算要注意
- 很可能bug就是一些小错误造成的
- 比如(nums[i] & xor) == 0
- 如果携程了 nums[i] & xoe == 0 就错误了

###Java Random
####1. Using Math.random()
```java
double random = Math.random() * 50 + 1;
or
int random = (int )(Math.random() * 50 + 1);
```
This will give you value from 1 to 50 using Math.random()

Why?

random() method returns a random number between 0.0 and 0.999. So, you multiply it by 50, so upper limit becomes 0.0 to 49.95, when you add 1, it becomes 1.0 to 50.95, now when you you truncate to int, you get 1 to 50. (thanks to @rup in comments). leepoint's awesome writeup on both the approaches.

####2. Using Random class in Java.
```java
Random rand = new Random();
int value = rand.nextInt(50); // 也可以使用rand.nextDouble() nextLong()
This will give value from 0 to 49.

For 1 to 50: rand.nextInt(50) + 1;
```

###Generic注意事项
####Generic array creation is disallowed in Java
```
Item[] a = new Item[capacity];
这样写就会错误了
要
Item[] a = (Item[]) new Object[capacity];
```

####ArrayList remove注意事项
	我们知道remove有两种
	一种是E remove(int index)
	一种是boolean remove(Object o)
	如果是Integer arraylist,将会自动调用remove(object o)
	这个时候就不要用remove来removeindex了
	list.remove(Integer.valueOf(2));
	list.remove(list.indexOf(2));
	You could use list.remove(new Integer(0)) to surely remove the object
	List<Integer> intList = new ArrayList<Integer>(Arrays.asList(intArray));

