# Rangoli Pattern Encoding

### Problem Statement

Ananya is designing a digital rangoli display system for a Diwali event in Varanasi. The system encodes messages in a zigzag pattern across multiple rows, then reads them row by row to create an encrypted display.

Given a string `message` and an integer `numRows`, arrange the characters in a zigzag pattern across the specified number of rows, then read line by line to produce the encoded string.

For example, "DIWALINIGHT" with 3 rows:
```
D   L   G
 I A I I H
  W   N   T
```
Reading row by row gives: "DLGIAIIHNWNT"

### Input Format

- The first line contains the string `message`.
- The second line contains an integer `numRows`.

### Output Format

- Print the zigzag encoded string.

### Constraints

- `1 <= message.length <= 1000`
- `1 <= numRows <= 1000`
- `message` consists of English letters, digits, commas, and periods

### Test Cases

#### Test Case 1
**Input:**
```
PAYPALISHIRING
3
```
**Output:**
```
PAHNAPLSIIGYIR
```
**Explanation:** 3 rows zigzag pattern. Row 0: P,A,H,N. Row 1: A,P,L,S,I,I,G. Row 2: Y,I,R. Concatenate rows to get "PAHNAPLSIIGYIR".

---

#### Test Case 2
**Input:**
```
PAYPALISHIRING
4
```
**Output:**
```
PINALSIGYAHRPI
```
**Explanation:** 4 rows zigzag. Row 0: P,I,N. Row 1: A,L,S,I,G. Row 2: Y,A,H,R. Row 3: P,I. Result = "PINALSIGYAHRPI".

---

#### Test Case 3
**Input:**
```
DIWALI
1
```
**Output:**
```
DIWALI
```
**Explanation:** Single row means no zigzag transformation. Output equals input.

---

#### Test Case 4
**Input:**
```
AB
1
```
**Output:**
```
AB
```
**Explanation:** Single row, string unchanged.

---

#### Test Case 5
**Input:**
```
ABCDE
2
```
**Output:**
```
ACEBD
```
**Explanation:** 2 rows zigzag. Row 0: A,C,E (indices 0,2,4). Row 1: B,D (indices 1,3). Result = "ACEBD".

---

#### Test Case 6
**Input:**
```
MUMBAI
3
```
**Output:**
```
MABUMI
```
**Explanation:** 3 rows. M(down)→row0, U(down)→row1, M(down)→row2, B(up)→row1, A(up)→row0, I(down)→row1. Row 0: M,A. Row 1: U,B,I. Row 2: M. Result = "MAUBIM".

---

#### Test Case 7
**Input:**
```
A
5
```
**Output:**
```
A
```
**Explanation:** Single character. numRows doesn't affect output. Result = "A".

---

### Solutions

#### Python

```python
class Solution:
    def encodeRangoli(self, message: str, numRows: int) -> str:
        # start your solution
        if numRows == 1 or numRows >= len(message):
            return message
        
        rows = [''] * numRows
        currentRow = 0
        goingDown = False
        
        for char in message:
            rows[currentRow] += char
            
            if currentRow == 0 or currentRow == numRows - 1:
                goingDown = not goingDown
            
            currentRow += 1 if goingDown else -1
        
        return ''.join(rows)
        # end your solution


def main():
    message = input().strip()
    numRows = int(input().strip())
    
    sol = Solution()
    result = sol.encodeRangoli(message, numRows)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

class Solution {
public:
    string encodeRangoli(string message, int numRows) {
        // start your solution
        if (numRows == 1 || numRows >= message.length()) {
            return message;
        }
        
        vector<string> rows(numRows);
        int currentRow = 0;
        bool goingDown = false;
        
        for (char c : message) {
            rows[currentRow] += c;
            
            if (currentRow == 0 || currentRow == numRows - 1) {
                goingDown = !goingDown;
            }
            
            currentRow += goingDown ? 1 : -1;
        }
        
        string result;
        for (string& row : rows) {
            result += row;
        }
        return result;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string message;
    int numRows;
    getline(cin, message);
    cin >> numRows;
    
    Solution sol;
    cout << sol.encodeRangoli(message, numRows) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public String encodeRangoli(String message, int numRows) {
        // start your solution
        if (numRows == 1 || numRows >= message.length()) {
            return message;
        }
        
        StringBuilder[] rows = new StringBuilder[numRows];
        for (int i = 0; i < numRows; i++) {
            rows[i] = new StringBuilder();
        }
        
        int currentRow = 0;
        boolean goingDown = false;
        
        for (char c : message.toCharArray()) {
            rows[currentRow].append(c);
            
            if (currentRow == 0 || currentRow == numRows - 1) {
                goingDown = !goingDown;
            }
            
            currentRow += goingDown ? 1 : -1;
        }
        
        StringBuilder result = new StringBuilder();
        for (StringBuilder row : rows) {
            result.append(row);
        }
        return result.toString();
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String message = sc.nextLine().trim();
        int numRows = Integer.parseInt(sc.nextLine().trim());
        
        Solution sol = new Solution();
        System.out.println(sol.encodeRangoli(message, numRows));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def encodeRangoli(self, message: str, numRows: int) -> str:
        # start your solution
        
        
        
        # end your solution


def main():
    message = input().strip()
    numRows = int(input().strip())
    
    sol = Solution()
    result = sol.encodeRangoli(message, numRows)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

class Solution {
public:
    string encodeRangoli(string message, int numRows) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string message;
    int numRows;
    getline(cin, message);
    cin >> numRows;
    
    Solution sol;
    cout << sol.encodeRangoli(message, numRows) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public String encodeRangoli(String message, int numRows) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String message = sc.nextLine().trim();
        int numRows = Integer.parseInt(sc.nextLine().trim());
        
        Solution sol = new Solution();
        System.out.println(sol.encodeRangoli(message, numRows));
        
        sc.close();
    }
}
```
