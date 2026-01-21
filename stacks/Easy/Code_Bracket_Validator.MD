# Code Bracket Validator

### Problem Statement

At Infosys Development Center in Mysuru, the code review system needs to validate that all brackets in code snippets are properly matched. The system must check if every opening bracket has a corresponding closing bracket in the correct order.

Given a string `code` containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

### Input Format

- A single line containing a string of brackets.

### Output Format

- Print `true` if valid, otherwise `false`.

### Constraints

- `1 <= code.length <= 10^4`
- `code` consists of parentheses only '()[]{}'

### Test Cases

#### Test Case 1
**Input:**
```
()
```
**Output:**
```
true
```
**Explanation:** Single pair of parentheses, properly matched.

---

#### Test Case 2
**Input:**
```
()[]{}
```
**Output:**
```
true
```
**Explanation:** Three pairs, each properly matched in sequence.

---

#### Test Case 3
**Input:**
```
(]
```
**Output:**
```
false
```
**Explanation:** Opening '(' doesn't match closing ']'.

---

#### Test Case 4
**Input:**
```
([)]
```
**Output:**
```
false
```
**Explanation:** Brackets interleaved incorrectly. '[' should close before ')'.

---

#### Test Case 5
**Input:**
```
{[]}
```
**Output:**
```
true
```
**Explanation:** Nested brackets properly matched. Inner '[]' closed before outer '{}'.

---

#### Test Case 6
**Input:**
```
(
```
**Output:**
```
false
```
**Explanation:** Unclosed opening bracket.

---

#### Test Case 7
**Input:**
```
(({{[[]]}}))
```
**Output:**
```
true
```
**Explanation:** Multiple nested brackets, all properly matched.

---

### Solutions

#### Python

```python
class Solution:
    def isValid(self, code: str) -> bool:
        # start your solution
        stack = []
        mapping = {')': '(', '}': '{', ']': '['}
        
        for char in code:
            if char in mapping:
                # Closing bracket
                if not stack or stack[-1] != mapping[char]:
                    return False
                stack.pop()
            else:
                # Opening bracket
                stack.append(char)
        
        return len(stack) == 0
        # end your solution


def main():
    code = input().strip()
    
    sol = Solution()
    result = sol.isValid(code)
    print("true" if result else "false")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <stack>
#include <string>
#include <unordered_map>
using namespace std;

class Solution {
public:
    bool isValid(string code) {
        // start your solution
        stack<char> stk;
        unordered_map<char, char> mapping = {{')', '('}, {'}', '{'}, {']', '['}};
        
        for (char c : code) {
            if (mapping.find(c) != mapping.end()) {
                // Closing bracket
                if (stk.empty() || stk.top() != mapping[c]) {
                    return false;
                }
                stk.pop();
            } else {
                // Opening bracket
                stk.push(c);
            }
        }
        
        return stk.empty();
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string code;
    getline(cin, code);
    
    Solution sol;
    cout << (sol.isValid(code) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public boolean isValid(String code) {
        // start your solution
        Stack<Character> stack = new Stack<>();
        Map<Character, Character> mapping = new HashMap<>();
        mapping.put(')', '(');
        mapping.put('}', '{');
        mapping.put(']', '[');
        
        for (char c : code.toCharArray()) {
            if (mapping.containsKey(c)) {
                // Closing bracket
                if (stack.isEmpty() || stack.peek() != mapping.get(c)) {
                    return false;
                }
                stack.pop();
            } else {
                // Opening bracket
                stack.push(c);
            }
        }
        
        return stack.isEmpty();
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String code = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.isValid(code) ? "true" : "false");
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def isValid(self, code: str) -> bool:
        # start your solution
        
        
        
        # end your solution


def main():
    code = input().strip()
    
    sol = Solution()
    result = sol.isValid(code)
    print("true" if result else "false")


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <stack>
#include <string>
#include <unordered_map>
using namespace std;

class Solution {
public:
    bool isValid(string code) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string code;
    getline(cin, code);
    
    Solution sol;
    cout << (sol.isValid(code) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public boolean isValid(String code) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String code = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.isValid(code) ? "true" : "false");
        
        sc.close();
    }
}
```
