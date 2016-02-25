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

####sort reverse order
	对于array与arraylist
	Arrays.sort(arraylist, Collections.reverseOrder());
	Collections.sort(arraylist, Collections.reverseOrder());

####使用二进制运算要注意
- 很可能bug就是一些小错误造成的
- 比如(nums[i] & xor) == 0
- 如果携程了 nums[i] & xoe == 0 就错误了
