###Some Common Use

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

####使用二进制运算要注意
- 很可能bug就是一些小错误造成的
- 比如(nums[i] & xor) == 0
- 如果携程了 nums[i] & xoe == 0 就错误了
