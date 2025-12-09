# Java String Methods – Complete List

> Comprehensive list of all `String` methods in Java 21.

---

## 🔹 Basic Info Methods

| Method | Description |
|--------|-------------|
| `charAt(int index)` | Returns the character at the specified index |
| `length()` | Returns the number of characters in the string |
| `isEmpty()` | Returns true if string length is 0 |
| `isBlank()` | Returns true if string is empty or contains only whitespace |
| `strip()` | Removes leading and trailing Unicode whitespace |
| `stripLeading()` | Removes only leading whitespace |
| `stripTrailing()` | Removes only trailing whitespace |
| `trim()` | Removes leading and trailing ASCII whitespace |
| `toLowerCase()` | Converts string to lowercase |
| `toLowerCase(Locale locale)` | Converts string to lowercase using given locale |
| `toUpperCase()` | Converts string to uppercase |
| `toUpperCase(Locale locale)` | Converts string to uppercase using given locale |

---

## 🔹 Comparison Methods

| Method | Description |
|--------|-------------|
| `equals(Object another)` | Compares two strings for exact equality (case-sensitive) |
| `equalsIgnoreCase(String another)` | Compares two strings for equality ignoring case |
| `compareTo(String another)` | Lexicographically compares two strings |
| `compareToIgnoreCase(String another)` | Lexicographically compares ignoring case |
| `contentEquals(CharSequence cs)` | Checks if string content equals given CharSequence |
| `contentEquals(StringBuffer sb)` | Checks if string content equals given StringBuffer |
| `matches(String regex)` | Checks if string matches regex |
| `regionMatches(int toffset, String other, int ooffset, int len)` | Checks if region of string matches region of another string |
| `regionMatches(boolean ignoreCase, int toffset, String other, int ooffset, int len)` | Same as above, ignoring case if true |

---

## 🔹 Searching Methods

| Method | Description |
|--------|-------------|
| `contains(CharSequence s)` | Returns true if string contains the given sequence |
| `startsWith(String prefix)` | Returns true if string starts with prefix |
| `startsWith(String prefix, int offset)` | Returns true if string starts with prefix at given index |
| `endsWith(String suffix)` | Returns true if string ends with suffix |
| `indexOf(int ch)` | Returns first index of character, -1 if not found |
| `indexOf(int ch, int fromIndex)` | Returns first index of character from given index |
| `indexOf(String str)` | Returns first index of substring, -1 if not found |
| `indexOf(String str, int fromIndex)` | Returns first index of substring from given index |
| `lastIndexOf(int ch)` | Returns last index of character |
| `lastIndexOf(int ch, int fromIndex)` | Returns last index of character starting from given index |
| `lastIndexOf(String str)` | Returns last index of substring |
| `lastIndexOf(String str, int fromIndex)` | Returns last index of substring from given index |

---

## 🔹 Substring & Subsequence

| Method | Description |
|--------|-------------|
| `substring(int beginIndex)` | Returns substring from beginIndex to end |
| `substring(int beginIndex, int endIndex)` | Returns substring from beginIndex to endIndex (exclusive) |
| `subSequence(int beginIndex, int endIndex)` | Returns a CharSequence for the specified range |

---

## 🔹 Modification & Transformation

| Method | Description |
|--------|-------------|
| `concat(String str)` | Concatenates string at the end |
| `replace(char oldChar, char newChar)` | Replaces all occurrences of oldChar with newChar |
| `replace(CharSequence target, CharSequence replacement)` | Replaces all occurrences of target with replacement |
| `replaceAll(String regex, String replacement)` | Replaces all substrings matching regex |
| `replaceFirst(String regex, String replacement)` | Replaces first substring matching regex |
| `repeat(int count)` | Repeats string count times |
| `indent(int n)` | Adds/removes n spaces at the start of each line |
| `transform(Function<? super String, ? extends R> f)` | Applies a transformation function |
| `intern()` | Returns string from the pool |

---

## 🔹 Splitting & Joining

| Method | Description |
|--------|-------------|
| `split(String regex)` | Splits string into array using regex |
| `split(String regex, int limit)` | Splits string into array with limit |
| `static join(CharSequence delimiter, CharSequence... elements)` | Joins elements with delimiter |
| `static join(CharSequence delimiter, Iterable<? extends CharSequence> elements)` | Joins iterable elements with delimiter |

---

## 🔹 Conversion Methods

| Method | Description |
|--------|-------------|
| `valueOf(boolean b)` | Converts boolean to String |
| `valueOf(char c)` | Converts char to String |
| `valueOf(char[] data)` | Converts char array to String |
| `valueOf(char[] data, int offset, int count)` | Converts portion of char array to String |
| `valueOf(double d)` | Converts double to String |
| `valueOf(float f)` | Converts float to String |
| `valueOf(int i)` | Converts int to String |
| `valueOf(long l)` | Converts long to String |
| `valueOf(Object obj)` | Converts object to String |

---

## 🔹 Streams & Lines

| Method | Description |
|--------|-------------|
| `chars()` | Returns IntStream of character codes |
| `codePoints()` | Returns IntStream of Unicode code points |
| `lines()` | Returns Stream of lines in string |

---

## 🔹 Character Access

| Method | Description |
|--------|-------------|
| `codePointAt(int index)` | Returns Unicode code point at index |
| `codePointBefore(int index)` | Returns Unicode code point before index |
| `codePointCount(int beginIndex, int endIndex)` | Counts code points between indices |
| `getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin)` | Copies substring into char array |
| `getBytes()` | Returns byte array of string in default charset |
| `getBytes(Charset charset)` | Returns byte array in specified charset |
| `getBytes(String charsetName)` | Returns byte array in specified charset name |
| `offsetByCodePoints(int index, int codePointOffset)` | Returns index after moving codePointOffset code points |

---

## 🔹 Formatting

| Method                                            | Description                       |
| ------------------------------------------------- | --------------------------------- |
| `format(String format, Object... args)`           | Formats string using placeholders |
| `format(Locale l, String format, Object... args)` | Formats string using locale       |

---

## 🔹 Miscellaneous

| Method | Description |
|--------|-------------|
| `copyValueOf(char[] data)` | Returns string from char array |
| `copyValueOf(char[] data, int offset, int count)` | Returns string from portion of char array |
| `toCharArray()` | Converts string to char array |
| `toString()` | Returns string itself |
