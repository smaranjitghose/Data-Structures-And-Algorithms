# Chat Message Cleanup

### Problem Statement

At a tech startup in Gurugram, the messaging app team is developing a feature to clean up accidental duplicate keystrokes. When users type too fast, they often press the same key twice. The system should repeatedly remove adjacent duplicate characters until no more can be removed.

Given a string `message`, remove all adjacent duplicate letters and return the final cleaned string.

### Input Format

- A single line containing a lowercase string.

### Output Format

- Print the cleaned string after removing all adjacent duplicates.

### Constraints

- `1 <= message.length <= 10^5`
- `message` consists of lowercase English letters only

### Test Cases

#### Test Case 1
**Input:**
```
abbaca
```
**Output:**
```
ca
```
**Explanation:** Remove "bb" → "aaca". Remove "aa" → "ca". No more adjacent duplicates.

---

#### Test Case 2
**Input:**
```
azxxzy
```
**Output:**
```
ay
```
**Explanation:** Remove "xx" → "azzy". Remove "zz" → "ay". No more adjacent duplicates.

---

#### Test Case 3
**Input:**
```
abc
```
**Output:**
```
abc
```
**Explanation:** No adjacent duplicates. String unchanged.

---

#### Test Case 4
**Input:**
```
aa
```
**Output:**
```

```
**Explanation:** Remove "aa" → empty string.

---

#### Test Case 5
**Input:**
```
aababaab
```
**Output:**
```
ba
```
**Explanation:** Remove adjacent pairs step by step until "ba" remains.

---

#### Test Case 6
**Input:**
```
abccba
```
**Output:**
```

```
**Explanation:** Remove "cc" → "abba". Remove "bb" → "aa". Remove "aa" → empty.

---

#### Test Case 7
**Input:**
```
mississippi
```
**Output:**
```
m
```
**Explanation:** Repeatedly remove adjacent duplicates until only "m" remains.

---

### Solutions

#### Python

```python
class Solution:
    def removeDuplicates(self, message: str) -> str:
        # start your solution
        stack = []
        
        for char in message:
            if stack and stack[-1] == char:
                stack.pop()
            else:
                stack.append(char)
        
        return ''.join(stack)
        # end your solution


def main():
    message = input().strip()
    
    sol = Solution()
    result = sol.removeDuplicates(message)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <string>
using namespace std;

class Solution {
public:
    string removeDuplicates(string message) {
        // start your solution
        string stack = "";
        
        for (char c : message) {
            if (!stack.empty() && stack.back() == c) {
                stack.pop_back();
            } else {
                stack.push_back(c);
            }
        }
        
        return stack;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string message;
    getline(cin, message);
    
    Solution sol;
    cout << sol.removeDuplicates(message) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public String removeDuplicates(String message) {
        // start your solution
        StringBuilder stack = new StringBuilder();
        
        for (char c : message.toCharArray()) {
            if (stack.length() > 0 && stack.charAt(stack.length() - 1) == c) {
                stack.deleteCharAt(stack.length() - 1);
            } else {
                stack.append(c);
            }
        }
        
        return stack.toString();
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String message = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.removeDuplicates(message));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def removeDuplicates(self, message: str) -> str:
        # start your solution
        
        
        
        # end your solution


def main():
    message = input().strip()
    
    sol = Solution()
    result = sol.removeDuplicates(message)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <string>
using namespace std;

class Solution {
public:
    string removeDuplicates(string message) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string message;
    getline(cin, message);
    
    Solution sol;
    cout << sol.removeDuplicates(message) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public String removeDuplicates(String message) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String message = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.removeDuplicates(message));
        
        sc.close();
    }
}
```
