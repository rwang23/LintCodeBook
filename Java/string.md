#String

```java
//String 是不能通过concat来改变的,除非赋值给一个新的String
String s = "Hello";
s.concat(" World!");//s本来是null
System.out.println(s);

String s1 = new String();
String s2 = "billryan";
int s2Len = s2.length();
s2.substring(4, 8); // return "ryan"
StringBuilder sb = new StringBuilder(s2.substring(4, 8));
sb.append("bill");
sb.deleteCharAt(int index);
sb.setLength(sb.length() - 1);

sb.delete(int start, int end);
String s2New = sb.toString(); // return "ryanbill"
// convert String to char array
char[] s2Char = s2.toCharArray();

// convert char arrays to string
	char[] myString = new char[] {'T', 'H', 'I', 'S', ' ',  'I', 'S', ' ', 'T', 'E', 'S', 'T'};

		String output1 = new String(myString);
		System.out.println("output1 : " + output1);

		String output2 = String.valueOf(myString);
		System.out.println("\noutput2 : " + output2);

// char at index 4
char ch = s2.charAt(4); // return 'r'
// find index at first
int index = s2.indexOf('r'); // return 4. if not found, return -1
```
####substring O(n)
- 使用substring这个函数其实是O(n)时间复杂度,所以不要直接用,而是记录下Index就好了

####StringBuilder insert
insert(index, char)
 result.insert(0, cur)
###String[] arrays 转化成string
Arrays.toString();
####注意判断string的时候
自己判断空的substring的时候,用的是 str == null
但是其实应该用str.equals(""),空是"",而不是null

###StringBuffer 与 StringBuilder, 前者保证线程安全，后者不是，但单线程下效率高一些，一般使用 StringBuilder.
###判断string是否相等 用.equals()
####== tests for reference equality (whether they are the same object).
####.equals() tests for value equality (whether they are logically "equal").

	char[] array
	for (char c : array) {

	}
	这个loop里边,c是array的copy,不是直接的array,
	所以改变每个c的值并不改变array
	要改变还是用for (int i = 0; i < array.length; i++) {
		array[i] = xx;
	}

####Replace
- This method returns a new string resulting from replacing all occurrences of oldChar in this string with newChar.

```java
import java.io.*;

public class Test{
   public static void main(String args[]){
      String Str = new String("Welcome to Tutorialspoint.com");

      System.out.print("Return Value :" );
      System.out.println(Str.replace('o', 'T'));

      System.out.print("Return Value :" );
      System.out.println(Str.replace('l', 'D'));
   }
}
This produces the following result:

Return Value :WelcTme tT TutTrialspTint.cTm
Return Value :WeDcome to TutoriaDspoint.com
```

####replaceAll
- This method replaces each substring of this string that matches the given regular expression with the given replacement.

```java
public class Test{
   public static void main(String args[]){
      String Str = new String("Welcome to Tutorialspoint.com");

      System.out.print("Return Value :" );
      System.out.println(Str.replaceAll("(.*)Tutorials(.*)",
                         "AMROOD" ));
   }
}
```

####Trim
- This method returns a copy of the string, with leading and trailing whitespace omitted.

```java
public class Test{
   public static void main(String args[]){
      String Str = new String("   Welcome to Tutorialspoint.com   ");

      System.out.print("Return Value :" );
      System.out.println(Str.trim() );
   }
}
This produces the following result:

Return Value :Welcome to Tutorialspoint.com
```

####Character Methods:
- 1) isLetter() Determines whether the specified char value is a letter.
- 2) isDigit() Determines whether the specified char value is a digit.
- 3) isWhitespace() Determines whether the specified char value is white space.
- 4) isUpperCase() Determines whether the specified char value is uppercase.
- 5) isLowerCase() Determines whether the specified char value is lowercase.
- 6) toUpperCase() Returns the uppercase form of the specified char value.
- 7) toLowerCase() Returns the lowercase form of the specified char value.
- 8) toString() Returns a String object representing the specified character valuethat is, a one-character string

####escape
- \n Newline. Position the screen cursor at the beginning of the next line.
- \t Horizontal tab. Move the screen cursor to the next tab stop.
- \r Carriage return. Position the screen cursor at the beginning of the current lineódo not advance to the next line. Any characters output after the carriagereturn overwrite the characters previously output on that line.
- \\ Backslash. Used to print a backslash character.
- \" Double quote. Used to print a double-quote character. For example


###Regular Expression
####Repetion
+ means one or more
* means zero or more
| means or
[123] match any character in the set
[1-3] range 1-3
^ excludes others


	String text = "Hello  hello?";
	String[] words = text.split(" +")
	//match one or more space


####Concatenation
得到word
[a-zA-Z]+
得到sentence
[^.!?]+


####wrapper class
- Predefined classes hv been defined to represent the primtive datatypes in the form of object
is called as Wrapper Classes.

```java
class A {
   public static void main(String[] args) {
      String str="100";
      //String str="hello"; //java.lang.NumberFormatException
      Integer i=new Integer(str);
      System.out.println(i);//Number formatException
   }
}
```
#####String to int(not Integer)
```
byte byteValue()--->The value of the specified number as a byte
short shortValue()--->The value of the specified number as a short
long longValue()--->The value of the specified number as a long
int intValue()--->The value of the specified number as a int
double doubleValue()--->The value of the specified number as a double
float floatValue()--->The value of the specified number as a float
```

```java
class A {
   public static void main(String[] args) {
      String str="100";
      Integer i=new Integer(str);
      System.out.println(i);//100
      int d=i.intValue();
      System.out.println(d);//100
   }
}
```
#####Integer.parseInt() Double.parseDouble() to convert String to int and doulbe
- static method

```java

   public static void main(String args[]){
      int x =Integer.parseInt("9");
      double c = Double.parseDouble("5");
      int b = Integer.parseInt("444",16);
      System.out.println(x);
      System.out.println(c);
      System.out.println(b);
   }
```
