# Java String Interview Questions (100)

## Basics
1. What is a `String` in Java?
2. Is `String` a primitive data type in Java?
3. Why is `String` immutable in Java?
4. How is `String` stored in the JVM memory?
5. What is the difference between `String` and `StringBuilder`?
6. What is the difference between `String` and `StringBuffer`?
7. Can two `String` objects with the same value point to the same reference?
8. What is the **String Constant Pool**?
9. How does the `==` operator work with Strings?
10. What is the difference between `==` and `.equals()` in Strings?

## Creation
11. How do you create a `String` in Java?
```
int[] arr = new int[]{1,2,3};
```
11. What is the difference between creating a String using `new` and using literals?
```
When we create String useing letteral JVM check if string already in the bool so it use it but when we use key word **new** its creating new object or strign object everytime we use new keyword. 
```
11. What happens when you concatenate two string literals?
```
concat happen at compiling time, other concat happen at run time. use concating  string letterals is butter and fast than using concat method. 
```
11. How does `String.intern()` method work?
```
- When you call `s.intern()`:
    
    - If the pool already contains a string equal to `s` (checked using `equals()`), then the reference to that string from the pool is returned.
        
    - If not, `s` is added to the pool, and then its reference is returned.
        
- This ensures that all interned strings with the same content point to **the same memory reference**.
```
11. Can we use `String` as a key in a `HashMap`? Why?
```
- `HashMap` requires that the key type properly implements:
    
    - `equals()` → to check key equality
        
    - `hashCode()` → to determine bucket placement
        
- `String` in Java **already overrides both `equals()` and `hashCode()`** in a way that makes it efficient and reliable for use as keys.
```
11. String builder and string literal using plus sign (+) 
```
using string builder use method append() is faster than using (+) sigin in string literals 
```

## Common Methods
16. What does the `length()` method return?
17. How do you compare two Strings ignoring case?
```
equalsIgnoreCase()
or use toLowerCase()/toUpperCase() for both and then compare them. 
eg: 
s1.toLowerCase().equals(s2.toLowerCase())
```
16. How do you extract a substring from a String?
```
s.substring(start, end);
s.substring(index);
```
16. How do you split a String in Java?
```
String[] parts = str.split(String regex);
String[] parts = str.split(String regex, int limit);
eg:
String text = "Java is fun";
String[] words = text.split(" ");
or
String fruits = "apple,banana,orange";
String[] arr = fruits.split(",");
or
String data = "one,two;three four";
String[] parts = data.split("[,; ]");
or
String line = "a:b:c:d";
String[] arr = line.split(":", 2);
in this case:
System.out.println(Arrays.toString(arr));
output: [a, b:c:d]//we have in this case array of two elements.

### ⚠️ Important Notes

- Since `split()` uses **regex**, special characters like `.`, `|`, `?`, `*`, `+` must be **escaped** if you want literal matching.
  "a.b.c".split("\\.");  // split by dot → [a, b, c]
Note: use \\ for scape:
So for regex metacharacters (`.`, `|`, `*`, `+`, `?`, `(`, `)`, `[`, `]`, `{`, `}`, `^`, `$`, and `\` itself), you often need **double escaping**.

for each singel scape char we need double \\
eg:
String text = "a\\\\\\b";     // actual string is: a\\\b
String[] parts = text.split("\\\\\\\\\\");


eg:
String path = "C:\\Users\\Mohammed";
String[] parts = path.split("\\\\");  

System.out.println(Arrays.toString(parts));
output: [C:, Users, Mohammed]
```
16. How do you replace characters in a String?
17. What does `trim()` method do?
18. How to check if a String contains a substring?
19. How to check if a String starts with or ends with another String?
20. How to convert a String to upper case and lower case?
21. How do you find the index of a substring?

## String Operations
26. What happens when you use `+` with Strings?
27. Which is faster: String concatenation using `+` or `StringBuilder`?
28. What is `concat()` method in String?
29. How do you reverse a String?
30. How to check if a String is palindrome?
31. How to count vowels and consonants in a String?
32. How to remove whitespace from a String?
33. How to remove duplicate characters from a String?
34. How to find the frequency of each character in a String?
35. How to find the first non-repeated character in a String?

## Conversion
36. How do you convert a String to an array of characters?
37. How do you convert a String to an `int`?
38. How do you convert a String to a `double`?
39. How do you convert an `int` to a String?
40. How do you convert a `char[]` to a String?
41. How to convert a String to a `byte[]`?
42. How to convert a String to `StringBuilder`?
43. How to convert a String to `StringBuffer`?
44. How do you parse a String to `LocalDate`?
45. How do you format numbers into Strings?

## Searching
46. How to check if a String contains only digits?
47. How to check if a String contains only letters?
48. How to check if a String contains alphanumeric characters?
49. How to find how many times a substring appears in a String?
50. How to find duplicate words in a String?

## Performance
51. Why should we prefer `StringBuilder` over String concatenation in loops?
52. What is the impact of immutability of String on memory?
53. What are memory leaks related to Substring in older Java versions?
54. How does Garbage Collector treat Strings?
55. How to improve performance when dealing with large Strings?

## Regular Expressions
56. How do you validate an email using a regex with String?
57. How to validate if a String contains only numbers using regex?
58. How do you replace multiple whitespaces with a single space?
59. How do you split a String using regex?
60. How to extract digits from a String using regex?

## Advanced
61. What is the difference between `matches()` and `contains()`?
62. What is `regionMatches()` method in String?
63. What is `compareTo()` method used for?
64. What is the difference between `compareTo()` and `equals()`?
65. Can Strings be used in switch statements?
66. How is `hashCode()` implemented in String class?
67. What is the significance of immutability in multi-threading for Strings?
68. Can we subclass `String` class?
69. Why is `String` class marked `final`?
70. How is String concatenation optimized by the compiler?

## Practical
71. Write a program to reverse words in a sentence.
72. Write a program to check if two Strings are anagrams.
73. Write a program to count the number of words in a String.
74. Write a program to find the longest word in a sentence.
75. Write a program to swap two Strings without using a third variable.
76. Write a program to check if two Strings are rotations of each other.
77. Write a program to check if two Strings are permutations of each other.
78. Write a program to print all substrings of a String.
79. Write a program to print the longest palindrome substring.
80. Write a program to find the maximum occurring character in a String.

## Edge Cases
81. What happens if you call `substring()` with invalid indexes?
82. What happens if you call `charAt()` with an index out of range?
83. Can a String be `null`? What happens if you call a method on it?
84. What is the difference between empty String `""` and `null` String?
85. How to safely compare two Strings that may be null?
86. What is the result of `"abc" + null`?
87. How do you check if a String is empty?
88. How do you check if a String is blank?
89. How to prevent `NullPointerException` in String operations?
90. What happens if you use `intern()` excessively?

## Miscellaneous
91. How to convert String to `UUID`?
92. How to convert String to `BigDecimal`?
93. What is the difference between `split()` and `StringTokenizer`?
94. How do you format Strings with placeholders (e.g., `%s`)?
95. What is the difference between `String.format()` and `MessageFormat`?
96. What is `join()` method in String?
97. What is `repeat()` method in String (Java 11+)?
98. What is the difference between `strip()` and `trim()` (Java 11+)?
99. How do you create a multiline String (text block) in Java 15+?
100. What are some best practices for working with Strings in Java?
# Java String Interview Questions (Set 2)

This note contains **100 different interview questions about Strings in Java**.  
These cover fundamentals, performance, memory handling, methods, and tricky scenarios.

---

## Core Concepts

1. What is the difference between `String`, `StringBuffer`, and `StringBuilder`?
2. Why are `String` objects immutable in Java?
3. What is the significance of the `final` keyword in the `String` class?
4. How does Java optimize memory for `String` objects?
5. What is the `String Constant Pool` (SCP)?
6. Explain how `intern()` method works in Strings.
7. What happens when you use `new String("abc")` vs `"abc"`?
8. Can two different `String` objects have the same hashcode?
9. What is the default encoding used for `String.getBytes()`?
10. Why is `String` immutable but `char[]` mutable?

---

## String Methods

11. What does the `equalsIgnoreCase()` method do?
12. Difference between `substring()` and `subSequence()`?
13. How does `split()` method handle regex patterns?
14. How can you reverse a `String` in Java?
15. What does `String.trim()` do internally?
16. How does `replaceAll()` differ from `replace()`?
17. Can `indexOf()` return negative values?
18. Explain the difference between `matches()` and `contains()`.
19. What does `String.join()` do?
20. How do you format Strings with `String.format()`?

---

## String Operations

21. What is string concatenation in Java?
22. Which is faster: `String.concat()` or `+` operator?
23. Explain how the `+` operator is implemented for Strings.
24. Why should you avoid `+` operator inside loops with Strings?
25. How does `StringBuilder` improve concatenation performance?
26. What happens when you concatenate `null` with a `String`?
27. What does `"abc" + 1 + 2` evaluate to?
28. What does `1 + 2 + "abc"` evaluate to?
29. How to efficiently build large dynamic Strings?
30. How does `StringBuffer` ensure thread-safety?

---

## String Comparison

31. What is the difference between `==` and `equals()` for Strings?
32. Why does `"abc" == "abc"` sometimes return `true`?
33. Can two Strings with the same value be stored at different memory locations?
34. What is lexicographical comparison of Strings?
35. How does `compareTo()` handle case sensitivity?
36. How to compare Strings ignoring case and whitespace?
37. Why is `equals()` case-sensitive for Strings?
38. What is the difference between `regionMatches()` and `startsWith()`?
39. How to check if two Strings are anagrams?
40. How to check if a String is a palindrome?

---

## Memory & Performance

41. Explain memory allocation when creating Strings.
42. What is String interning?
43. How does garbage collection work with Strings?
44. Why is creating Strings with `new` discouraged?
45. How to reduce memory usage with large Strings?
46. What is the difference between heap and SCP Strings?
47. What happens when you call `intern()` on a String already in SCP?
48. How does Java optimize String literals at compile-time?
49. How do String constants affect class loading?
50. How does substring() work internally before Java 7 and after?

---

## Advanced String Handling

51. How to convert a String to a `char[]`?
52. How to convert `char[]` to a String?
53. How to find the frequency of characters in a String?
54. How to remove duplicate characters from a String?
55. How to count vowels and consonants in a String?
56. How to find the first non-repeated character in a String?
57. How to find the first repeated character in a String?
58. How to remove whitespace from a String?
59. How to extract numbers from a String?
60. How to split a String into lines?

---

## Regular Expressions & Strings

61. How to validate an email using regex in a String?
62. How to validate a phone number?
63. How to check if a String contains only digits?
64. How to check if a String contains only alphabets?
65. How to extract words from a sentence?
66. How to remove all special characters from a String?
67. How does `Pattern.compile()` optimize regex usage with Strings?
68. How to replace multiple spaces with a single space?
69. How to validate a strong password using regex?
70. How to check if a String matches a date format?

---

## Practical Use Cases

71. How to convert a String to an `int`?
72. How to convert an `int` to a String?
73. How to convert a String to a `double`?
74. How to convert a String to a `boolean`?
75. How to convert a String to `LocalDate`?
76. How to check if a String is empty?
77. Difference between `isEmpty()` and `isBlank()`?
78. How to remove a specific character from a String?
79. How to check if a String starts with a given prefix?
80. How to check if a String ends with a given suffix?

---

## Tricky & Edge Cases

81. What happens if you call `substring(0, length())`?
82. What does `substring(0,0)` return?
83. Can `null` be assigned to a String variable?
84. What happens when you call methods on a null String reference?
85. How to handle NullPointerException with Strings safely?
86. Why is `String` not a primitive type?
87. How to sort a String array alphabetically?
88. How to sort a String by characters?
89. How does String hashcode calculation work?
90. How to implement a custom String pool?

---

## Miscellaneous

91. What is the maximum length of a String in Java?
92. How does String serialization work?
93. Why is String popular as a key in HashMap?
94. Why is String used in Class loading?
95. What is String deduplication in JVM?
96. How to convert a String to a `List<Character>`?
97. How to join a List of Strings into one String?
98. How to count words in a String?
99. How to remove HTML tags from a String?
100. How to reverse words in a String?

---

✅ These 100 questions are focused on **Strings in Java**, covering fundamentals, advanced handling, memory, regex, and tricky interview scenarios.


# Java String Interview Questions - Set 3

Here’s a fresh set of 100 unique questions on **Strings in Java** for interviews.

---

## Basics
1. What is the difference between `String`, `StringBuffer`, and `StringBuilder` in Java?
2. Why are `String` objects immutable in Java?
3. How are string literals stored in the string pool?
4. What is the difference between `new String("abc")` and `"abc"`?
5. What happens when you use the `+` operator with strings in Java?
6. How is string concatenation optimized by the compiler?
7. Can two different string objects have the same hashcode?
8. Explain interning of strings in Java.
9. How is the `equals()` method different from `==` in strings?
10. What happens if you compare a string with `null`?

---

## String Operations
11. How do you reverse a string in Java?
12. How do you check if a string is a palindrome?
13. How do you count vowels and consonants in a string?
14. How can you find the first non-repeating character in a string?
15. How do you remove all spaces from a string?
16. How do you split a string by a delimiter?
17. How do you join multiple strings in Java?
18. How do you check if a string contains only digits?
19. How do you check if two strings are anagrams?
20. How do you remove duplicate characters from a string?

---

## String Methods
21. Explain the use of `substring()` method.
22. How do you convert a string to uppercase and lowercase?
23. How does `replace()` differ from `replaceAll()`?
24. How do you trim leading and trailing spaces from a string?
25. How does `compareTo()` work for strings?
26. What is the difference between `contains()` and `matches()`?
27. How does `indexOf()` behave if the character is not found?
28. What does `lastIndexOf()` return if no match is found?
29. How do you split a string into an array of characters?
30. How do you extract digits from a string?

---

## Advanced String Questions
31. How do you find the longest substring without repeating characters?
32. How do you find the longest palindromic substring?
33. How do you count the frequency of each character in a string?
34. How do you remove consecutive duplicate characters?
35. How do you reverse words in a string without using extra space?
36. How do you capitalize the first letter of each word in a string?
37. How do you count occurrences of a substring?
38. How do you find the lexicographically smallest substring?
39. How do you check if one string is a rotation of another?
40. How do you compress a string using character counts?

---

## String and Regular Expressions
41. How do you validate an email using regex?
42. How do you check if a string contains only alphabets using regex?
43. How do you extract numbers from a string using regex?
44. How do you replace multiple spaces with a single space using regex?
45. How do you validate a phone number with regex?
46. How do you find all words that start with a capital letter?
47. How do you check if a string is a valid date format?
48. How do you split a string by multiple delimiters using regex?
49. How do you remove special characters using regex?
50. How do you validate a strong password using regex?

---

## Performance & Memory
51. Why is string concatenation in loops discouraged?
52. How does `StringBuilder` improve performance?
53. What is the internal representation of a `String` in Java 9 and later?
54. What happens when you call `intern()` on a string?
55. What are memory implications of creating strings with `new`?
56. How does garbage collection work with string pool?
57. Why should we avoid excessive use of string concatenation?
58. How do string operations affect performance in large applications?
59. What is the difference in memory usage between string literals and new strings?
60. When should you use `StringBuffer` over `StringBuilder`?

---

## Conversion
61. How do you convert a string to an integer?
62. How do you convert an integer to a string?
63. How do you convert a string to a character array?
64. How do you convert a character array back to a string?
65. How do you convert a string to a byte array?
66. How do you convert a byte array back to a string?
67. How do you parse a string to a double?
68. How do you format a number into a string?
69. How do you convert a string to a list of characters?
70. How do you convert a string to a set of characters?

---

## String Algorithms
71. How do you check if one string is a subsequence of another?
72. How do you implement string rotation without using extra space?
73. How do you check if a string contains another string without using `contains()`?
74. How do you generate all substrings of a string?
75. How do you find the longest common prefix among strings?
76. How do you check if a string is made of repeating substrings?
77. How do you count the number of words in a string?
78. How do you count the number of sentences in a string?
79. How do you check if a string matches a wildcard pattern?
80. How do you reverse only vowels in a string?

---

## Real-World Scenarios
81. How do you mask credit card numbers in a string?
82. How do you extract domain name from an email?
83. How do you remove HTML tags from a string?
84. How do you validate a URL using regex?
85. How do you generate random strings in Java?
86. How do you format strings with placeholders?
87. How do you escape special characters in JSON strings?
88. How do you encode a string to Base64?
89. How do you decode a Base64 string?
90. How do you validate filenames and paths?

---

## Trick & Edge Cases
91. What happens if you call `charAt()` with an invalid index?
92. Can a string have a `null` value?
93. What does `String.valueOf(null)` return?
94. How do you compare two null strings safely?
95. How do you find the length of an empty string?
96. What happens if you split an empty string?
97. How do you handle strings with Unicode characters?
98. What is the difference between `length` of array and `length()` of string?
99. How do you check if two strings are equal ignoring case?
100. What is the result of `"abc".substring(0, 3)`?

---

# 📌 Summary
This is **Set 3 of 100 unique Java String interview questions** (different from Set 1 and Set 2).  
They cover **basics, operations, methods, regex, memory, algorithms, real-world scenarios, and edge cases**.

---
# Java String Interview Questions – Set 4

This is the **fourth set** of 100 **Java String interview questions**, all different from Set 1, Set 2, and Set 3.  

---

## General String Concepts

1. What is string immutability and why is it important?  
2. How does immutability improve security in Java Strings?  
3. How does immutability improve caching of Strings?  
4. Can you create a mutable String in Java?  
5. What class provides a mutable alternative to String?  
6. How does the JVM internally represent String?  
7. What does the `intern()` method do?  
8. Is `intern()` method useful for memory optimization?  
9. What is the difference between `new String("abc")` and `"abc"`?  
10. How many objects are created with `new String("abc")`?  

---

## String Pool

11. What is the String Pool in Java?  
12. Where is the String Pool stored in memory?  
13. Is the String Pool garbage-collected?  
14. How does `intern()` relate to the String Pool?  
15. Are Strings stored in the pool automatically?  
16. What is the difference between String Pool in Java 6 and Java 7+?  
17. Can String Pool reduce memory leaks?  
18. How does the JVM optimize memory with String Pool?  
19. What happens when two strings with the same literal are created?  
20. Is String Pool a part of the heap or stack?  

---

## String Creation & Initialization

21. How many ways can we create a String in Java?  
22. Which is preferred: `"abc"` or `new String("abc")`?  
23. What does `String.valueOf()` return?  
24. Can we initialize a String using `char[]`?  
25. Can you convert `byte[]` to String?  
26. How can you create a String from `InputStream`?  
27. How can you create a String from `StringBuffer`?  
28. What happens if you assign `null` to a String?  
29. Is `String s = null;` valid?  
30. Can Strings be declared as `final`?  

---

## String Methods (Core)

31. What does `String.length()` return?  
32. What does `String.isEmpty()` check?  
33. Difference between `isBlank()` and `isEmpty()`?  
34. What does `String.charAt()` return?  
35. What does `String.indexOf()` return if not found?  
36. Difference between `indexOf()` and `lastIndexOf()`?  
37. How does `String.contains()` work internally?  
38. How do you extract a substring?  
39. Can `substring()` cause memory leaks?  
40. What does `trim()` remove?  

---

## String Comparisons

41. Difference between `equals()` and `==` for Strings?  
42. Is `equalsIgnoreCase()` safe for Unicode?  
43. How does `compareTo()` work?  
44. What does `compareToIgnoreCase()` return?  
45. What happens if you compare a String with `null`?  
46. Is `equals()` case-sensitive?  
47. Which is faster: `equals()` or `==`?  
48. Can you use `Objects.equals()` for Strings?  
49. What is lexicographical comparison?  
50. How does String hashing work in HashMap?  

---

## String Mutations

51. What does `concat()` do?  
52. Is `concat()` faster than `+`?  
53. Can `+` operator create performance issues?  
54. How is `+` operator compiled by the JVM?  
55. Why should `StringBuilder` be preferred over `+` in loops?  
56. How does `replace()` differ from `replaceAll()`?  
57. Difference between `replaceFirst()` and `replace()`?  
58. Does `replaceAll()` use regex?  
59. Can `StringBuffer` be converted to `String`?  
60. How do you reverse a String without using `StringBuilder`?  

---

## String Formatting & Conversion

61. What does `String.format()` do?  
62. Difference between `String.format()` and `MessageFormat`?  
63. What is `%s`, `%d`, `%f` in `String.format()`?  
64. How does `String.join()` work?  
65. What does `String.join()` return for empty input?  
66. Can you use `String.format()` for date/time?  
67. How do you convert `String` to `int`?  
68. How do you convert `String` to `double`?  
69. How do you convert `int` to `String`?  
70. How do you convert `char[]` to String?  

---

## String Splitting & Tokens

71. How does `String.split()` work?  
72. What does `split()` return for an empty String?  
73. Difference between `split()` and `StringTokenizer`?  
74. Can `split()` handle regex?  
75. What happens if regex is invalid in `split()`?  
76. What does `limit` parameter in `split()` mean?  
77. How does `split()` behave with multiple delimiters?  
78. What is the output of `"abc".split("")`?  
79. Can `split()` return empty tokens?  
80. How does `Pattern.splitAsStream()` differ from `split()`?  

---

## String & Performance

81. Why are Strings immutable in Java?  
82. How does immutability improve HashMap keys performance?  
83. Why is `String` a popular HashMap key?  
84. What are memory implications of String concatenation?  
85. Is `StringBuilder` faster than `StringBuffer`?  
86. Why should String concatenation be avoided in loops?  
87. Can String objects be garbage collected?  
88. What is the impact of large String objects on memory?  
89. How does String interning improve performance?  
90. Can improper String handling cause memory leaks?  

---

## Advanced String Questions

91. How does `regionMatches()` work?  
92. What does `matches()` do?  
93. Does `matches()` use regex internally?  
94. Difference between `matches()` and `contains()`?  
95. What does `codePointAt()` return?  
96. What is the purpose of `codePointCount()`?  
97. What does `offsetByCodePoints()` do?  
98. How to check if String contains only digits?  
99. How to check if String contains only letters?  
100. How to check if String is a valid palindrome?  

---

# ✅ Summary

This **Set 4** provides **100 unique interview questions** on Java Strings covering:  
- String Pool  
- Creation & Initialization  
- Core methods  
- Comparisons  
- Mutations  
- Formatting & Conversions  
- Splitting & Tokens  
- Performance  
- Advanced methods  


