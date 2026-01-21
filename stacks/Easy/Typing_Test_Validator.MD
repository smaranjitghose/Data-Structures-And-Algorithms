# Typing Test Validator

### Problem Statement

At TCS iON's recruitment portal in Chennai, candidates take a typing test. The system records keystrokes where '#' represents a backspace. Two candidates' submissions need to be compared to check if they result in the same final text.

Given two strings `typing1` and `typing2`, return `true` if they are equal when both are typed into empty text editors, otherwise return `false`. The '#' character means a backspace (delete the previous character).

Note: After backspacing an empty text, the text remains empty.

### Input Format

- The first line contains the first typing string.
- The second line contains the second typing string.

### Output Format

- Print `true` if both result in same text, otherwise `false`.

### Constraints

- `1 <= typing1.length, typing2.length <= 200`
- `typing1` and `typing2` only contain lowercase letters and '#' characters

### Test Cases

#### Test Case 1
**Input:**
```
ab#c
ad#c
```
**Output:**
```
true
```
**Explanation:** Both result in "ac". typing1: a→ab→a→ac. typing2: a→ad→a→ac.

---

#### Test Case 2
**Input:**
```
ab##
c#d#
```
**Output:**
```
true
```
**Explanation:** Both result in "". typing1: a→ab→a→(empty). typing2: c→(empty)→d→(empty).

---

#### Test Case 3
**Input:**
```
a#c
b
```
**Output:**
```
false
```
**Explanation:** typing1 results in "c". typing2 results in "b". Not equal.

---

#### Test Case 4
**Input:**
```
abc
abc
```
**Output:**
```
true
```
**Explanation:** No backspaces. Both are "abc".

---

#### Test Case 5
**Input:**
```
a##b
b
```
**Output:**
```
true
```
**Explanation:** typing1: a→(empty, extra # ignored)→b. typing2: b. Both equal "b".

---

#### Test Case 6
**Input:**
```
hello###lo
helo#lo
```
**Output:**
```
true
```
**Explanation:** typing1: hello→hell→hel→he→helo. typing2: helo→hel→helo. Both result in "helo".

---

#### Test Case 7
**Input:**
```
xy#z
xzz#
```
**Output:**
```
true
```
**Explanation:** typing1: x→xy→x→xz. typing2: x→xz→xzz→xz. Both equal "xz".

---

### Solutions

#### Python

```python
class Solution:
    def backspaceCompare(self, typing1: str, typing2: str) -> bool:
        # start your solution
        def processTyping(s: str) -> str:
            stack = []
            for char in s:
                if char == '#':
                    if stack:
                        stack.pop()
                else:
                    stack.append(char)
            return ''.join(stack)
        
        return processTyping(typing1) == processTyping(typing2)
        # end your solution


def main():
    typing1 = input().strip()
    typing2 = input().strip()
    
    sol = Solution()
    result = sol.backspaceCompare(typing1, typing2)
    print("true" if result else "false")


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
    bool backspaceCompare(string typing1, string typing2) {
        // start your solution
        return processTyping(typing1) == processTyping(typing2);
        // end your solution
    }
    
private:
    string processTyping(const string& s) {
        string stack = "";
        for (char c : s) {
            if (c == '#') {
                if (!stack.empty()) {
                    stack.pop_back();
                }
            } else {
                stack.push_back(c);
            }
        }
        return stack;
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string typing1, typing2;
    getline(cin, typing1);
    getline(cin, typing2);
    
    Solution sol;
    cout << (sol.backspaceCompare(typing1, typing2) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public boolean backspaceCompare(String typing1, String typing2) {
        // start your solution
        return processTyping(typing1).equals(processTyping(typing2));
        // end your solution
    }
    
    private String processTyping(String s) {
        StringBuilder stack = new StringBuilder();
        for (char c : s.toCharArray()) {
            if (c == '#') {
                if (stack.length() > 0) {
                    stack.deleteCharAt(stack.length() - 1);
                }
            } else {
                stack.append(c);
            }
        }
        return stack.toString();
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String typing1 = sc.nextLine();
        String typing2 = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.backspaceCompare(typing1, typing2) ? "true" : "false");
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def backspaceCompare(self, typing1: str, typing2: str) -> bool:
        # start your solution
        
        
        
        # end your solution


def main():
    typing1 = input().strip()
    typing2 = input().strip()
    
    sol = Solution()
    result = sol.backspaceCompare(typing1, typing2)
    print("true" if result else "false")


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
    bool backspaceCompare(string typing1, string typing2) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string typing1, typing2;
    getline(cin, typing1);
    getline(cin, typing2);
    
    Solution sol;
    cout << (sol.backspaceCompare(typing1, typing2) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public boolean backspaceCompare(String typing1, String typing2) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String typing1 = sc.nextLine();
        String typing2 = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.backspaceCompare(typing1, typing2) ? "true" : "false");
        
        sc.close();
    }
}
```
