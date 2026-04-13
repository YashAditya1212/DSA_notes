Java Strings
Slicing, Splicing & Built-in Methods — Complete Reference
1. What is a String?
A String in Java is an immutable sequence of characters. Once created, its value cannot be changed. Strings are objects of the java.lang.String class.

Two ways to create a String:
```java
String s1 = "Hello";             // String literal (stored in String Pool)
String s2 = new String("Hello"); // New object on heap (avoid this)
```

Key characteristics:
•	Immutable — any modification returns a new String object
•	Stored in the String Pool for memory efficiency
•	Use StringBuilder for mutable string operations (e.g., in loops)
•	== compares references; always use .equals() to compare content
2. String Slicing
Slicing means extracting a portion of a string. In Java, slicing is done using the substring() method.
```java
Index positions work like this:
"H"  "e"  "l"  "l"  "o"  " "  "W"  "o"  "r"  "l"  "d"
 0    1    2    3    4    5    6    7    8    9   10

substring(int startIndex)
Extracts from startIndex to the end of the string.
"Hello World".substring(6);    // "World"
"Hello World".substring(0);    // "Hello World"

substring(int startIndex, int endIndex)
Extracts from startIndex (inclusive) to endIndex (exclusive).
"Hello World".substring(0, 5); // "Hello"
"Hello World".substring(3, 8); // "lo Wo"

split(String regex)
Splits string into an array around matches of the regex pattern.
String[] parts = "a,b,c".split(",");   // ["a", "b", "c"]
String[] words = "Hi there".split(" "); // ["Hi", "there"]

toCharArray()
Converts the string into a character array — another form of slicing per character.
char[] arr = "Hello".toCharArray();
// arr = ['H', 'e', 'l', 'l', 'o']
```

3. String Splicing
Splicing means combining, joining, or inserting content into strings.

Using + (Concatenation Operator)
String result = "Hello" + " " + "World"; // "Hello World"
```java
concat()
"Hello".concat(" World"); // "Hello World"

String.join()
Best for joining multiple strings with a delimiter.
String.join(", ", "Java", "Python", "C++"); // "Java, Python, C++"
String.join("-", "2024", "01", "15");        // "2024-01-15"

String.format()
Structured string building using format specifiers.
String.format("Name: %s, Age: %d", "Ali", 25);
// "Name: Ali, Age: 25"

StringBuilder (for mutable splicing)
Use StringBuilder when building strings in loops for better performance.
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");   // "Hello World"
sb.insert(5, ",");     // "Hello, World"
sb.delete(5, 6);       // "Hello World"
String result = sb.toString();

4. All Built-in String Methods
4.1 Inspection Methods
Method	Description	Example
length()	Returns number of characters	"Hello".length() → 5
isEmpty()	Returns true if length is 0	"".isEmpty() → true
isBlank()	True if empty or whitespace (Java 11+)	"  ".isBlank() → true
charAt(int i)	Returns char at index i	"Hello".charAt(1) → 'e'
indexOf(String s)	First index of substring, -1 if not found	"banana".indexOf("an") → 1
lastIndexOf(String s)	Last occurrence index of substring	"banana".lastIndexOf("an") → 3
contains(CharSeq s)	True if string contains the sequence	"Hello".contains("ell") → true
startsWith(String s)	True if string starts with prefix	"Hello".startsWith("He") → true
endsWith(String s)	True if string ends with suffix	"Hello".endsWith("lo") → true
matches(String re)	True if matches regex pattern	"123".matches("\\d+") → true
codePointAt(int i)	Returns Unicode code point at index	"A".codePointAt(0) → 65
```
4.2 Slicing Methods
Method	Description	Example
```java
substring(int s)	Substring from index to end	"Hello".substring(2) → "llo"
substring(int s, int e)	Substring from s (incl.) to e (excl.)	"Hello".substring(1,4) → "ell"
split(String re)	Split by regex into String[]	"a,b".split(",") → ["a","b"]
split(String re, int n)	Split into at most n parts	"a,b,c".split(",",2) → ["a","b,c"]
toCharArray()	Returns char[] of all characters	"Hi".toCharArray() → ['H','i']
chars()	Returns IntStream of char values (Java 8+)	"ab".chars() → IntStream 97,98
```

4.3 Splicing / Building Methods
Method	Description	Example
```java
concat(String s)	Appends string to end	"Hi".concat("!") → "Hi!"
replace(char,char)	Replaces all occurrences of char	"aabb".replace('b','x') → "aaxx"
replace(seq,seq)	Replaces all occurrences of substring	"Hello World".replace("World","Java")
replaceAll(re,str)	Replaces all regex matches	"a1b2".replaceAll("\\d","*") → "a*b*"
replaceFirst(re,str)	Replaces first regex match only	"a1b2".replaceFirst("\\d","*") → "a*b2"
String.join(del,strs)	Static: joins strings with delimiter	String.join("-","a","b") → "a-b"
String.format(fmt,...)	Static: formatted string output	String.format("%s=%d","x",5) → "x=5"
repeat(int n)	Repeats string n times (Java 11+)	"ab".repeat(3) → "ababab"
formatted(args...)	Instance format (Java 15+)	"Hello %s".formatted("World")
intern()	Returns string from String Pool	new String("hi").intern()
```

4.4 Case & Whitespace Methods
Method	Description	Example
```java
toUpperCase()	All characters to uppercase	"hello".toUpperCase() → "HELLO"
toLowerCase()	All characters to lowercase	"HELLO".toLowerCase() → "hello"
trim()	Removes leading/trailing ASCII spaces	"  hi  ".trim() → "hi"
strip()	Removes Unicode whitespace (Java 11+)	"  hi  ".strip() → "hi"
stripLeading()	Removes leading whitespace only	"  hi  ".stripLeading() → "hi  "
stripTrailing()	Removes trailing whitespace only	"  hi  ".stripTrailing() → "  hi"
indent(int n)	Adjusts indentation of lines (Java 12+)	"hi".indent(4) → "    hi\n"
lines()	Returns stream of lines (Java 11+)	"a\nb".lines() → Stream["a","b"]
```
4.5 Comparison Methods
Method	Description	Example
```java
equals(Object o)	Case-sensitive content equality	"hi".equals("hi") → true
equalsIgnoreCase(s)	Case-insensitive equality	"Hi".equalsIgnoreCase("HI") → true
compareTo(String s)	Lexicographic comparison (0 = equal)	"apple".compareTo("apple") → 0
compareToIgnoreCase(s)	Case-insensitive lexicographic compare	"A".compareToIgnoreCase("a") → 0
regionMatches(...)	Compares a region of two strings	"Hello".regionMatches(1,"ello",0,4)
contentEquals(seq)	Compares with CharSequence/StringBuilder	"hi".contentEquals(new StringBuilder("hi"))
```

4.6 Conversion Methods
Method	Description	Example
```java
String.valueOf(x)	Static: converts primitive to String	String.valueOf(42) → "42"
getBytes()	Encodes string to byte array	"Hi".getBytes() → byte[]
getBytes(Charset c)	Encodes with specific charset	"Hi".getBytes(StandardCharsets.UTF_8)
toString()	Returns the string itself	"Hello".toString() → "Hello"
```

5. Quick Tips & Common Mistakes
•	Always use .equals() not == to compare string content.
•	substring(s, e) → end index is EXCLUSIVE. "Hello".substring(0,5) is "Hello" not "Hello "
•	Use StringBuilder in loops — concatenating with + in a loop creates many objects.
•	strip() (Java 11+) is better than trim() as it handles all Unicode whitespace.
•	String.valueOf(x) is the safest way to convert any type to String.
•	indexOf() returns -1 when not found — always check before using the result.
Java Strings
Slicing, Splicing & Built-in Methods — Complete Reference
1. What is a String?
A String in Java is an immutable sequence of characters. Once created, its value cannot be changed. Strings are objects of the java.lang.String class.

Two ways to create a String:
String s1 = "Hello";             // String literal (stored in String Pool)
String s2 = new String("Hello"); // New object on heap (avoid this)

Key characteristics:
•	Immutable — any modification returns a new String object
•	Stored in the String Pool for memory efficiency
•	Use StringBuilder for mutable string operations (e.g., in loops)
•	== compares references; always use .equals() to compare content
2. String Slicing
Slicing means extracting a portion of a string. In Java, slicing is done using the substring() method.
```java
Index positions work like this:
"H"  "e"  "l"  "l"  "o"  " "  "W"  "o"  "r"  "l"  "d"
 0    1    2    3    4    5    6    7    8    9   10

substring(int startIndex)
Extracts from startIndex to the end of the string.
"Hello World".substring(6);    // "World"
"Hello World".substring(0);    // "Hello World"

substring(int startIndex, int endIndex)
Extracts from startIndex (inclusive) to endIndex (exclusive).
"Hello World".substring(0, 5); // "Hello"
"Hello World".substring(3, 8); // "lo Wo"

split(String regex)
Splits string into an array around matches of the regex pattern.
String[] parts = "a,b,c".split(",");   // ["a", "b", "c"]
String[] words = "Hi there".split(" "); // ["Hi", "there"]

toCharArray()
Converts the string into a character array — another form of slicing per character.
char[] arr = "Hello".toCharArray();
// arr = ['H', 'e', 'l', 'l', 'o']
```

3. String Splicing
Splicing means combining, joining, or inserting content into strings.
```java
Using + (Concatenation Operator)
String result = "Hello" + " " + "World"; // "Hello World"

concat()
"Hello".concat(" World"); // "Hello World"

String.join()
Best for joining multiple strings with a delimiter.
String.join(", ", "Java", "Python", "C++"); // "Java, Python, C++"
String.join("-", "2024", "01", "15");        // "2024-01-15"

String.format()
Structured string building using format specifiers.
String.format("Name: %s, Age: %d", "Ali", 25);
// "Name: Ali, Age: 25"

StringBuilder (for mutable splicing)
Use StringBuilder when building strings in loops for better performance.
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");   // "Hello World"
sb.insert(5, ",");     // "Hello, World"
sb.delete(5, 6);       // "Hello World"
String result = sb.toString();
```
4. All Built-in String Methods
4.1 Inspection Methods
Method	Description	Example
```java
length()	Returns number of characters	"Hello".length() → 5
isEmpty()	Returns true if length is 0	"".isEmpty() → true
isBlank()	True if empty or whitespace (Java 11+)	"  ".isBlank() → true
charAt(int i)	Returns char at index i	"Hello".charAt(1) → 'e'
indexOf(String s)	First index of substring, -1 if not found	"banana".indexOf("an") → 1
lastIndexOf(String s)	Last occurrence index of substring	"banana".lastIndexOf("an") → 3
contains(CharSeq s)	True if string contains the sequence	"Hello".contains("ell") → true
startsWith(String s)	True if string starts with prefix	"Hello".startsWith("He") → true
endsWith(String s)	True if string ends with suffix	"Hello".endsWith("lo") → true
matches(String re)	True if matches regex pattern	"123".matches("\\d+") → true
codePointAt(int i)	Returns Unicode code point at index	"A".codePointAt(0) → 65
```
4.2 Slicing Methods
Method	Description	Example
```java
substring(int s)	Substring from index to end	"Hello".substring(2) → "llo"
substring(int s, int e)	Substring from s (incl.) to e (excl.)	"Hello".substring(1,4) → "ell"
split(String re)	Split by regex into String[]	"a,b".split(",") → ["a","b"]
split(String re, int n)	Split into at most n parts	"a,b,c".split(",",2) → ["a","b,c"]
toCharArray()	Returns char[] of all characters	"Hi".toCharArray() → ['H','i']
chars()	Returns IntStream of char values (Java 8+)	"ab".chars() → IntStream 97,98
```

4.3 Splicing / Building Methods
Method	Description	Example
```java
concat(String s)	Appends string to end	"Hi".concat("!") → "Hi!"
replace(char,char)	Replaces all occurrences of char	"aabb".replace('b','x') → "aaxx"
replace(seq,seq)	Replaces all occurrences of substring	"Hello World".replace("World","Java")
replaceAll(re,str)	Replaces all regex matches	"a1b2".replaceAll("\\d","*") → "a*b*"
replaceFirst(re,str)	Replaces first regex match only	"a1b2".replaceFirst("\\d","*") → "a*b2"
String.join(del,strs)	Static: joins strings with delimiter	String.join("-","a","b") → "a-b"
String.format(fmt,...)	Static: formatted string output	String.format("%s=%d","x",5) → "x=5"
repeat(int n)	Repeats string n times (Java 11+)	"ab".repeat(3) → "ababab"
formatted(args...)	Instance format (Java 15+)	"Hello %s".formatted("World")
intern()	Returns string from String Pool	new String("hi").intern()
```

4.4 Case & Whitespace Methods
Method	Description	Example
```java
toUpperCase()	All characters to uppercase	"hello".toUpperCase() → "HELLO"
toLowerCase()	All characters to lowercase	"HELLO".toLowerCase() → "hello"
trim()	Removes leading/trailing ASCII spaces	"  hi  ".trim() → "hi"
strip()	Removes Unicode whitespace (Java 11+)	"  hi  ".strip() → "hi"
stripLeading()	Removes leading whitespace only	"  hi  ".stripLeading() → "hi  "
stripTrailing()	Removes trailing whitespace only	"  hi  ".stripTrailing() → "  hi"
indent(int n)	Adjusts indentation of lines (Java 12+)	"hi".indent(4) → "    hi\n"
lines()	Returns stream of lines (Java 11+)	"a\nb".lines() → Stream["a","b"]
```

4.5 Comparison Methods
Method	Description	Example
```java
equals(Object o)	Case-sensitive content equality	"hi".equals("hi") → true
equalsIgnoreCase(s)	Case-insensitive equality	"Hi".equalsIgnoreCase("HI") → true
compareTo(String s)	Lexicographic comparison (0 = equal)	"apple".compareTo("apple") → 0
compareToIgnoreCase(s)	Case-insensitive lexicographic compare	"A".compareToIgnoreCase("a") → 0
regionMatches(...)	Compares a region of two strings	"Hello".regionMatches(1,"ello",0,4)
contentEquals(seq)	Compares with CharSequence/StringBuilder	"hi".contentEquals(new StringBuilder("hi"))
```

4.6 Conversion Methods
Method	Description	Example
```java
String.valueOf(x)	Static: converts primitive to String	String.valueOf(42) → "42"
getBytes()	Encodes string to byte array	"Hi".getBytes() → byte[]
getBytes(Charset c)	Encodes with specific charset	"Hi".getBytes(StandardCharsets.UTF_8)
toString()	Returns the string itself	"Hello".toString() → "Hello"
```
5. Quick Tips & Common Mistakes
•	Always use .equals() not == to compare string content.
•	substring(s, e) → end index is EXCLUSIVE. "Hello".substring(0,5) is "Hello" not "Hello "
•	Use StringBuilder in loops — concatenating with + in a loop creates many objects.
•	strip() (Java 11+) is better than trim() as it handles all Unicode whitespace.
•	String.valueOf(x) is the safest way to convert any type to String.
•	indexOf() returns -1 when not found — always check before using the result.
