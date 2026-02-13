```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);

        while (scan.hasNextLine()) {
            String line = scan.nextLine().trim();
            if (line.isEmpty()) continue;

            // Remove all numbers (int or double) from the line
            line = line.replaceAll("\\b\\d+(\\.\\d+)?\\b", "").trim();

            if (!line.isEmpty()) {
                System.out.println(line);
            }
        }

        scan.close();
    }
}

```
---
### 🔹 How it works

1. `nextLine()` → read **one line at a time**
    
2. `trim()` → remove leading/trailing whitespace
    
3. `replaceAll("\\b\\d+(\\.\\d+)?\\b", "")`
    
    - `\\b` → word boundary
        
    - `\\d+` → one or more digits
        
    - `(\\.\\d+)?` → optional decimal part
        
    - Removes all **numbers** (ints & doubles)
        
4. `trim()` again → clean spaces left by removed numbers
    
5. If line still has text → print it
    

---

### 🔹 Input

`32 hello world 3.4 test this is string 4`

### 🔹 Output

`hello world test this is string`

✅ Perfect — all numbers removed, text preserved.