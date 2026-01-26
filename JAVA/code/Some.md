```java
import java.util.*;

/*
========================================================
STRING CHARACTER INTERVIEW CHEAT SHEET
All scenarios in ONE place
- Uses ONLY for-loops
- No streams
- Clear interview-style logic
========================================================
*/

public class StringCharProblems {

    public static void main(String[] args) {

        /* ================================
           COMMON INPUTS
        ================================= */
        String str = "swiss";

        /* =================================================
           1️⃣ FREQUENCY ARRAY APPROACH (ASCII – FASTEST)
           ================================================= */

        // Create frequency array (ASCII)
        int[] freq = new int[256];

        // Populate frequency array
        for (char c : str.toCharArray()) {
            freq[c]++;
        }

        // 1.1 First Non-Repeating Character
        for (char c : str.toCharArray()) {
            if (freq[c] == 1) {
                System.out.println("First non-repeating: " + c);
                break;
            }
        }

        // 1.2 Most Repeated Character
        char maxChar = 0;
        int maxCount = 0;

        for (int i = 0; i < 256; i++) {
            if (freq[i] > maxCount) {
                maxCount = freq[i];
                maxChar = (char) i;
            }
        }
        System.out.println("Most repeated: " + maxChar);

        // 1.3 Check if All Characters Are Unique
        boolean allUnique = true;
        for (int count : freq) {
            if (count > 1) {
                allUnique = false;
                break;
            }
        }
        System.out.println("All characters unique: " + allUnique);

        // 1.4 Anagram Check (Array Method)
        String a = "listen";
        String b = "silent";

        int[] anagramArr = new int[256];

        for (char c : a.toCharArray()) anagramArr[c]++;
        for (char c : b.toCharArray()) anagramArr[c]--;

        boolean isAnagram = true;
        for (int count : anagramArr) {
            if (count != 0) {
                isAnagram = false;
                break;
            }
        }
        System.out.println("Anagram (array): " + isAnagram);

        /* =================================================
           2️⃣ MAP APPROACH (ORDER SAFE / UNICODE SAFE)
           ================================================= */

        // Create LinkedHashMap to preserve order
        Map<Character, Integer> map = new LinkedHashMap<>();

        // Populate map
        for (char c : str.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }

        // 2.1 First Non-Repeating Character
        for (Map.Entry<Character, Integer> entry : map.entrySet()) {
            if (entry.getValue() == 1) {
                System.out.println("First non-repeating (map): " + entry.getKey());
                break;
            }
        }

        // 2.2 Most Repeated Character
        char mapMaxChar = 0;
        int mapMaxCount = 0;

        for (Map.Entry<Character, Integer> entry : map.entrySet()) {
            if (entry.getValue() > mapMaxCount) {
                mapMaxCount = entry.getValue();
                mapMaxChar = entry.getKey();
            }
        }
        System.out.println("Most repeated (map): " + mapMaxChar);

        // 2.3 Check if All Characters Are Unique
        boolean mapAllUnique = true;
        for (int count : map.values()) {
            if (count > 1) {
                mapAllUnique = false;
                break;
            }
        }
        System.out.println("All characters unique (map): " + mapAllUnique);

        // 2.4 Anagram Check (Map Method)
        Map<Character, Integer> anaMap = new HashMap<>();

        for (char c : a.toCharArray())
            anaMap.put(c, anaMap.getOrDefault(c, 0) + 1);

        for (char c : b.toCharArray())
            anaMap.put(c, anaMap.get(c) - 1);

        boolean isAnagramMap = true;
        for (int count : anaMap.values()) {
            if (count != 0) {
                isAnagramMap = false;
                break;
            }
        }
        System.out.println("Anagram (map): " + isAnagramMap);
    }
}

```