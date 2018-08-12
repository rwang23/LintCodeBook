##Regular Expression
[参考教程](http://www.vogella.com/tutorials/JavaRegularExpressions/article.html)

###Match
|Regular Expression	|Description|
|---	|---	|
|.| Matches any character. |
|   ^regex | Finds regex that must match at the beginning of the line. |
|   regex$|   Finds regex that must match at the end of the line.|
|   [abc]|   Set definition, can match the letter a or b or c.|
|   [abc][vz] |   Set definition, can match a or b or c followed by either v or z.|
|   [^ abc]|   When a caret appears as the first character inside square brackets, it negates the pattern. This pattern matches any character except a or b or c.|
|   [a-d1-7]|   Ranges: matches a letter between a and d and figures from 1 to 7, but not d1.|
|   X|Z|   Finds X or Z.|
|   XZ|   Finds X directly followed by Z.|
|   $|   Checks if a line end follows.|


###Meta Characters
```
Regular Expression	Description
\d
Any digit, short for [0-9]
\D
A non-digit, short for [^0-9]
\s
A whitespace character, short for [ \t\n\x0b\r\f]
\S
A non-whitespace character, short for
\w
A word character, short for [a-zA-Z_0-9]
\W
A non-word character [^\w]
\S+
Several non-whitespace characters
\b
Matches a word boundary where a word character is [a-zA-Z0-9_]
```

###Quantifier
```
Regular Expression	Description	Examples
*
Occurs zero or more times, is short for {0,}
X* finds no or several letter X, <sbr /> .* finds any character sequence
+
Occurs one or more times, is short for {1,}
X+- Finds one or several letter X
?
Occurs no or one times, ? is short for {0,1}.
X? finds no or exactly one letter X
{X}
Occurs X number of times, {} describes the order of the preceding liberal
\d{3} searches for three digits, .{10} for any character sequence of length 10.
{X,Y}
Occurs between X and Y times,
\d{1,4} means \d must occur at least once and at a maximum of four.
*?
? after a quantifier makes it a reluctant quantifier. It tries to find the smallest match. This makes the regular expression stop at the first match.

```

###Backslashed in Java

The backslash \ is an escape character in Java Strings. That means backslash has a predefined meaning in Java. You have to use double backslash \\ to define a single backslash. If you want to define \w, then you must be using \\w in your regex. If you want to use backslash as a literal, you have to type \\\\ as \ is also an escape character in regular expressions.

###Method

```
s.matches("regex")
Evaluates if "regex" matches s. Returns only true if the WHOLE string can be matched.
s.split("regex")
Creates an array with substrings of s divided at occurrence of "regex". "regex" is not included in the result.
s.replaceFirst("regex"), "replacement"
Replaces first occurance of "regex" with "replacement.
s.replaceAll("regex"), "replacement"
Replaces all occurances of "regex" with "replacement.

lookingAt() method only matches the regular expression against the beginning of the tex

The Matcher find() method searches for occurrences of the regular expressions in the text passed to the Pattern.matcher(text) method

The methods start() and end() will give the indexes into the text where the found match starts and ends
```

###Code

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class RegexMatches {

   public static void main( String args[] ) {
      // String to be scanned to find the pattern.
      String line = "This order was placed for QT3000! OK?";
      String pattern = "(.*)(\\d+)(.*)";

      // Create a Pattern object
      Pattern r = Pattern.compile(pattern);

      // Now create matcher object.
      Matcher m = r.matcher(line);
      if (m.find( )) {
         System.out.println("Found value: " + m.group(0) );
         System.out.println("Found value: " + m.group(1) );
         System.out.println("Found value: " + m.group(2) );
      }else {
         System.out.println("NO MATCH");
      }
   }
}
```

###Matcher group
[参考](http://stackoverflow.com/questions/16517689/confused-about-matcher-group-in-java-regex)


The whole pattern is defined to be group number 0.

Any capturing group in the pattern start indexing from 1. The indices are defined by the order of the opening parentheses of the capturing groups. As an example, here are all 5 capturing groups in the below pattern:

```
(group)(?:non-capturing-group)(g(?:ro|u)p( (nested)inside)(another)group)(?=assertion)
|     |                       |          | |      |      ||       |     |
1-----1                       |          | 4------4      |5-------5     |
                              |          3---------------3              |
                              2-----------------------------------------2
```

The group numbers are used in back-reference \n in pattern and $n in replacement string.

In other regex flavors (PCRE, Perl), they can also be used in sub-routine calls.

You can access the text matched by certain group with Matcher.group(int group). The group numbers can be identified with the rule stated above.
