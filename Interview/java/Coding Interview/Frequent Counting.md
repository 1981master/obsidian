```java
// PRACTICE: FREQUENCY COUNT (JAVA)

/****************************
 * PROBLEM
 ****************************/

// Given a list of values, count how many times each value appears.

// Example:
// input: ["a", "b", "a", "c", "b", "a"]
// output:
// {
//   a=3,
//   b=2,
//   c=1
// }

/****************************
 * REQUIREMENTS
 ****************************/

// 1) First solve using a loop
// 2) Then solve using streams
// 3) Return a Map<String, Integer>

import java.util.*;
import java.util.stream.*;

public class Main {

    /****************************
     * YOUR CODE HERE
     ****************************/

    public static Map<String, Integer> countFreqLoop(List<String> list) {
        if (list == null) return new HashMap<>();

        Map<String, Integer> map = new HashMap<>();

        for (String s : list) {
            map.put(s, map.getOrDefault(s, 0) + 1);
        }

        return map;
    }

    public static Map<String, Integer> countFreqStream(List<String> list) {
        if (list == null) return new HashMap<>();

        // Correct stream solution using groupingBy + counting
        return list.stream()
                .filter(Objects::nonNull)
                .collect(Collectors.groupingBy(
                        s -> s,
                        Collectors.collectingAndThen(
                                Collectors.counting(),
                                Long::intValue
                        )
                ));
    }

    /****************************
     * TEST
     ****************************/

    public static void main(String[] args) {
        List<String> data = Arrays.asList("a", "b", "a", "c", "b", "a");

        System.out.println(countFreqLoop(data));
        System.out.println(countFreqStream(data));
    }
}

```