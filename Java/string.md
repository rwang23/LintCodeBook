#String

String 是不能通过concat来改变的,除非赋值给一个新的String
String s = "Hello";
s.concat(" World!");
System.out.println(s);

```java
String s1 = new String();
String s2 = "billryan";
int s2Len = s2.length();
s2.substring(4, 8); // return "ryan"
StringBuilder sb = new StringBuilder(s2.substring(4, 8));
sb.append("bill");
sb.deleteCharAt(int index);
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

