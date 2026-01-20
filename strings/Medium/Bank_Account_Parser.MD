# Bank Account Parser

### Problem Statement

Ravi works at a State Bank of India branch in Lucknow. He's building a system to parse account numbers from scanned documents where the text may contain leading whitespace, signs, and trailing non-numeric characters.

Given a string `document`, parse and return the integer value following these rules:

1. Ignore leading whitespace
2. Check for optional '+' or '-' sign
3. Read digits until a non-digit character or end of string
4. Clamp the result to 32-bit signed integer range [-2³¹, 2³¹ - 1]
5. Return 0 if no valid conversion can be performed

### Input Format

- A single line containing the string `document`.

### Output Format

- Print a single integer — the parsed value.

### Constraints

- `0 <= document.length <= 200`
- `document` consists of English letters, digits, spaces, and '+', '-', '.' characters

### Test Cases

#### Test Case 1
**Input:**
```
   42
```
**Output:**
```
42
```
**Explanation:** Skip 3 leading spaces. No sign found, default positive. Read digits '4' and '2'. Result = 42.

---

#### Test Case 2
**Input:**
```
   -42
```
**Output:**
```
-42
```
**Explanation:** Skip 3 leading spaces. Negative sign found. Read digits '4' and '2'. Apply sign. Result = -42.

---

#### Test Case 3
**Input:**
```
4193 with words
```
**Output:**
```
4193
```
**Explanation:** No leading whitespace. No sign. Read '4', '1', '9', '3'. Stop at space (non-digit). Result = 4193.

---

#### Test Case 4
**Input:**
```
words and 987
```
**Output:**
```
0
```
**Explanation:** First non-whitespace character 'w' is neither a digit nor a sign. Invalid input. Result = 0.

---

#### Test Case 5
**Input:**
```
-91283472332
```
**Output:**
```
-2147483648
```
**Explanation:** Negative sign found. Parsed value -91283472332 is less than -2³¹ (-2147483648). Clamp to INT_MIN. Result = -2147483648.

---

#### Test Case 6
**Input:**
```
+123
```
**Output:**
```
123
```
**Explanation:** Positive sign explicitly given. Read digits '1', '2', '3'. Result = 123.

---

#### Test Case 7
**Input:**
```
  +  413
```
**Output:**
```
0
```
**Explanation:** Skip 2 leading spaces. '+' sign found. Next character is space, not a digit. Invalid sequence. Result = 0.

---

### Solutions

#### Python

```python
class Solution:
    def parseAccount(self, document: str) -> int:
        # start your solution
        INT_MAX = 2**31 - 1
        INT_MIN = -2**31
        
        i = 0
        n = len(document)
        
        while i < n and document[i] == ' ':
            i += 1
        
        if i == n:
            return 0
        
        sign = 1
        if document[i] == '-':
            sign = -1
            i += 1
        elif document[i] == '+':
            i += 1
        
        result = 0
        while i < n and document[i].isdigit():
            digit = int(document[i])
            
            if result > (INT_MAX - digit) // 10:
                return INT_MAX if sign == 1 else INT_MIN
            
            result = result * 10 + digit
            i += 1
        
        return sign * result
        # end your solution


def main():
    document = input()
    
    sol = Solution()
    result = sol.parseAccount(document)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <string>
#include <climits>
using namespace std;

class Solution {
public:
    int parseAccount(string document) {
        // start your solution
        int i = 0, n = document.length();
        
        while (i < n && document[i] == ' ') {
            i++;
        }
        
        if (i == n) return 0;
        
        int sign = 1;
        if (document[i] == '-') {
            sign = -1;
            i++;
        } else if (document[i] == '+') {
            i++;
        }
        
        long result = 0;
        while (i < n && isdigit(document[i])) {
            result = result * 10 + (document[i] - '0');
            
            if (sign == 1 && result > INT_MAX) return INT_MAX;
            if (sign == -1 && -result < INT_MIN) return INT_MIN;
            
            i++;
        }
        
        return sign * result;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string document;
    getline(cin, document);
    
    Solution sol;
    cout << sol.parseAccount(document) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int parseAccount(String document) {
        // start your solution
        int i = 0, n = document.length();
        
        while (i < n && document.charAt(i) == ' ') {
            i++;
        }
        
        if (i == n) return 0;
        
        int sign = 1;
        if (document.charAt(i) == '-') {
            sign = -1;
            i++;
        } else if (document.charAt(i) == '+') {
            i++;
        }
        
        long result = 0;
        while (i < n && Character.isDigit(document.charAt(i))) {
            result = result * 10 + (document.charAt(i) - '0');
            
            if (sign == 1 && result > Integer.MAX_VALUE) return Integer.MAX_VALUE;
            if (sign == -1 && -result < Integer.MIN_VALUE) return Integer.MIN_VALUE;
            
            i++;
        }
        
        return (int)(sign * result);
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String document = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.parseAccount(document));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def parseAccount(self, document: str) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    document = input()
    
    sol = Solution()
    result = sol.parseAccount(document)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <string>
#include <climits>
using namespace std;

class Solution {
public:
    int parseAccount(string document) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string document;
    getline(cin, document);
    
    Solution sol;
    cout << sol.parseAccount(document) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int parseAccount(String document) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String document = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.parseAccount(document));
        
        sc.close();
    }
}
```
