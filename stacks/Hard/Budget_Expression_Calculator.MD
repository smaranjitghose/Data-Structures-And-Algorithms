# Budget Expression Calculator

### Problem Statement

The Finance Ministry in North Block, New Delhi uses a legacy system that evaluates budget expressions. The system needs to handle expressions containing digits, '+', '-', parentheses '(' and ')', and spaces.

Given a string `expression` representing a valid mathematical expression, implement a basic calculator to evaluate it and return the result.

Note: You are not allowed to use any built-in function which evaluates strings as mathematical expressions.

### Input Format

- A single line containing the mathematical expression string.

### Output Format

- Print the result of the expression evaluation.

### Constraints

- `1 <= expression.length <= 3 * 10^5`
- `expression` consists of digits, '+', '-', '(', ')', and spaces
- `expression` represents a valid expression
- '+' is not used as a unary operation (i.e., "+1" and "+(2 + 3)" are invalid)
- '-' could be used as a unary operation (i.e., "-1" and "-(2 + 3)" are valid)
- There will be no two consecutive operators in the input
- Every number and running calculation will fit in a signed 32-bit integer

### Test Cases

#### Test Case 1
**Input:**
```
1 + 1
```
**Output:**
```
2
```
**Explanation:** Simple addition. 1 + 1 = 2.

---

#### Test Case 2
**Input:**
```
 2-1 + 2 
```
**Output:**
```
3
```
**Explanation:** 2 - 1 + 2 = 3. Spaces are ignored.

---

#### Test Case 3
**Input:**
```
(1+(4+5+2)-3)+(6+8)
```
**Output:**
```
23
```
**Explanation:** Inner parentheses first: (4+5+2)=11, then (1+11-3)=9, then (6+8)=14. Total: 9+14=23.

---

#### Test Case 4
**Input:**
```
-2 + 1
```
**Output:**
```
-1
```
**Explanation:** Unary minus. -2 + 1 = -1.

---

#### Test Case 5
**Input:**
```
-(3 + 2) + 1
```
**Output:**
```
-4
```
**Explanation:** -(3+2) = -5. Then -5 + 1 = -4.

---

#### Test Case 6
**Input:**
```
10 + 20 - 5
```
**Output:**
```
25
```
**Explanation:** Multi-digit numbers. 10 + 20 - 5 = 25.

---

#### Test Case 7
**Input:**
```
((5 - 3) + (8 - 2))
```
**Output:**
```
8
```
**Explanation:** (5-3)=2, (8-2)=6. Total: 2+6=8.

---

### Solutions

#### Python

```python
class Solution:
    def calculate(self, expression: str) -> int:
        # start your solution
        stack = []
        num = 0
        sign = 1
        result = 0
        
        for char in expression:
            if char.isdigit():
                num = num * 10 + int(char)
            elif char == '+':
                result += sign * num
                num = 0
                sign = 1
            elif char == '-':
                result += sign * num
                num = 0
                sign = -1
            elif char == '(':
                # Push current result and sign onto stack
                stack.append(result)
                stack.append(sign)
                result = 0
                sign = 1
            elif char == ')':
                result += sign * num
                num = 0
                # Pop sign and previous result
                result *= stack.pop()  # sign before parenthesis
                result += stack.pop()  # previous result
        
        result += sign * num
        return result
        # end your solution


def main():
    expression = input()
    
    sol = Solution()
    result = sol.calculate(expression)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <stack>
#include <string>
using namespace std;

class Solution {
public:
    int calculate(string expression) {
        // start your solution
        stack<int> stk;
        int num = 0;
        int sign = 1;
        int result = 0;
        
        for (char c : expression) {
            if (isdigit(c)) {
                num = num * 10 + (c - '0');
            } else if (c == '+') {
                result += sign * num;
                num = 0;
                sign = 1;
            } else if (c == '-') {
                result += sign * num;
                num = 0;
                sign = -1;
            } else if (c == '(') {
                // Push current result and sign onto stack
                stk.push(result);
                stk.push(sign);
                result = 0;
                sign = 1;
            } else if (c == ')') {
                result += sign * num;
                num = 0;
                // Pop sign and previous result
                result *= stk.top(); stk.pop();  // sign before parenthesis
                result += stk.top(); stk.pop();  // previous result
            }
        }
        
        result += sign * num;
        return result;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string expression;
    getline(cin, expression);
    
    Solution sol;
    cout << sol.calculate(expression) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int calculate(String expression) {
        // start your solution
        Stack<Integer> stack = new Stack<>();
        int num = 0;
        int sign = 1;
        int result = 0;
        
        for (int i = 0; i < expression.length(); i++) {
            char c = expression.charAt(i);
            
            if (Character.isDigit(c)) {
                num = num * 10 + (c - '0');
            } else if (c == '+') {
                result += sign * num;
                num = 0;
                sign = 1;
            } else if (c == '-') {
                result += sign * num;
                num = 0;
                sign = -1;
            } else if (c == '(') {
                // Push current result and sign onto stack
                stack.push(result);
                stack.push(sign);
                result = 0;
                sign = 1;
            } else if (c == ')') {
                result += sign * num;
                num = 0;
                // Pop sign and previous result
                result *= stack.pop();  // sign before parenthesis
                result += stack.pop();  // previous result
            }
        }
        
        result += sign * num;
        return result;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String expression = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.calculate(expression));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def calculate(self, expression: str) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    expression = input()
    
    sol = Solution()
    result = sol.calculate(expression)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <stack>
#include <string>
using namespace std;

class Solution {
public:
    int calculate(string expression) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string expression;
    getline(cin, expression);
    
    Solution sol;
    cout << sol.calculate(expression) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int calculate(String expression) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String expression = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.calculate(expression));
        
        sc.close();
    }
}
```
