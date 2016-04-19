#String

## 基本

##### substring(a,b) 左闭右开

##### StringBuilder / StringBuffer 在后面添加使用 或者insert(index,char)
	s.append("s")

##### StringBuffer 与 StringBuilder, 前者保证线程安全，后者不是，但单线程下效率高一些，一般使用 StringBuilder.

##### StringBuilder / StringBuffer 变成String 用
	sb.toString()

##### String 变成CharArray
	char[] s2Char = s2.toCharArray()
- StringBuilder / StringBuffer 的话 String

##### CharArray to String 用
	chars[index] = c;
    String s =  new String(chars);
#### Integer to string
	Integer.toString(i)

#### Integer to Char
	- integer转化为char(只限于0-9) char key = (char) ('0' + k);

```java
String s1 = new String();
String s2 = "billryan";
int s2Len = s2.length();
s2.substring(4, 8); // return "ryan"
StringBuilder sb = new StringBuilder(s2.substring(4, 8));
sb.append("bill");
String s2New = sb.toString(); // return "ryanbill"
// convert String to char array
char[] s2Char = s2.toCharArray();
// char at index 4
char ch = s2.charAt(4); // return 'r'
// find index at first
int index = s2.indexOf('r'); // return 4. if not found, return -1
```

####替换String中的一个char
- 不能直接替换 如这样，charAt只能得到值，不能set

```java
String myName = "domanokz";
myName.charAt(4) = 'x';
```

- 只能这样

```java
String myName = "domanokz";
String newName = myName.substring(0,4)+'x'+myName.substring(5);
```
或者

```java
StringBuilder myName = new StringBuilder("domanokz");
myName.setCharAt(4, 'x');
```
