# Postfix Calculator

### Problem Statement

The tech team at Paytm in Noida is developing a scientific calculator feature. The backend processes expressions in Reverse Polish Notation (postfix notation) for efficient evaluation without parentheses.

Given an array of strings `tokens` representing an arithmetic expression in Reverse Polish Notation, evaluate the expression and return the result.

Valid operators are +, -, *, and /. Each operand may be an integer or another expression. Division truncates toward zero.

### Input Format

- The first line contains an integer `n`, the number of tokens.
- The second line contains `n` space-separated tokens (numbers and operators).

### Output Format

- Print the result of the expression.

### Constraints

- `1 <= n <= 10^4`
- `tokens[i]` is either an operator (+, -, *, /) or an integer in range [-200, 200]
- The input always represents a valid arithmetic expression
- The answer and all intermediate calculations fit in a 32-bit integer

### Test Cases

#### Test Case 1
**Input:**
```
5
2 1 + 3 *
```
**Output:**
```
9
```
**Explanation:** ((2 + 1) * 3) = 9. Push 2,1. Add → 3. Push 3. Multiply → 9.

---

#### Test Case 2
**Input:**
```
5
4 13 5 / +
```
**Output:**
```
6
```
**Explanation:** (4 + (13 / 5)) = 4 + 2 = 6. Division truncates 13/5 = 2.

---

#### Test Case 3
**Input:**
```
13
10 6 9 3 + -11 * / * 17 + 5 +
```
**Output:**
```
22
```
**Explanation:** Complex expression. Evaluate step by step using stack.

---

#### Test Case 4
**Input:**
```
1
42
```
**Output:**
```
42
```
**Explanation:** Single number, no operation needed.

---

#### Test Case 5
**Input:**
```
3
3 4 +
```
**Output:**
```
7
```
**Explanation:** Simple addition. 3 + 4 = 7.

---

#### Test Case 6
**Input:**
```
3
6 -3 *
```
**Output:**
```
-18
```
**Explanation:** Multiplication with negative. 6 * (-3) = -18.

---

#### Test Case 7
**Input:**
```
5
-7 2 / 3 +
```
**Output:**
```
0
```
**Explanation:** -7 / 2 = -3 (truncate toward zero). -3 + 3 = 0.

---

### Solutions

#### Python

```python
class Solution:
    def evalRPN(self, tokens: list[str]) -> int:
        # start your solution
        stack = []
        operators = {'+', '-', '*', '/'}
        
        for token in tokens:
            if token in operators:
                b = stack.pop()
                a = stack.pop()
                
                if token == '+':
                    stack.append(a + b)
                elif token == '-':
                    stack.append(a - b)
                elif token == '*':
                    stack.append(a * b)
                elif token == '/':
                    # Truncate toward zero
                    stack.append(int(a / b))
            else:
                stack.append(int(token))
        
        return stack[0]
        # end your solution


def main():
    n = int(input())
    tokens = input().split()
    
    sol = Solution()
    result = sol.evalRPN(tokens)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <string>
using namespace std;

class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        // start your solution
        stack<long long> stk;
        
        for (const string& token : tokens) {
            if (token == "+" || token == "-" || token == "*" || token == "/") {
                long long b = stk.top(); stk.pop();
                long long a = stk.top(); stk.pop();
                
                if (token == "+") stk.push(a + b);
                else if (token == "-") stk.push(a - b);
                else if (token == "*") stk.push(a * b);
                else if (token == "/") stk.push(a / b);  // C++ truncates toward zero
            } else {
                stk.push(stoll(token));
            }
        }
        
        return stk.top();
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<string> tokens(n);
    for (int i = 0; i < n; i++) {
        cin >> tokens[i];
    }
    
    Solution sol;
    cout << sol.evalRPN(tokens) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int evalRPN(String[] tokens) {
        // start your solution
        Stack<Long> stack = new Stack<>();
        
        for (String token : tokens) {
            if (token.equals("+") || token.equals("-") || 
                token.equals("*") || token.equals("/")) {
                long b = stack.pop();
                long a = stack.pop();
                
                if (token.equals("+")) stack.push(a + b);
                else if (token.equals("-")) stack.push(a - b);
                else if (token.equals("*")) stack.push(a * b);
                else if (token.equals("/")) stack.push(a / b);  // Java truncates toward zero
            } else {
                stack.push(Long.parseLong(token));
            }
        }
        
        return stack.pop().intValue();
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        String[] tokens = new String[n];
        
        for (int i = 0; i < n; i++) {
            tokens[i] = sc.next();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.evalRPN(tokens));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def evalRPN(self, tokens: list[str]) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    tokens = input().split()
    
    sol = Solution()
    result = sol.evalRPN(tokens)
    print(result)


if __name__ == "__main__":
    main()
```

#### C++

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <string>
using namespace std;

class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<string> tokens(n);
    for (int i = 0; i < n; i++) {
        cin >> tokens[i];
    }
    
    Solution sol;
    cout << sol.evalRPN(tokens) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int evalRPN(String[] tokens) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        String[] tokens = new String[n];
        
        for (int i = 0; i < n; i++) {
            tokens[i] = sc.next();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.evalRPN(tokens));
        
        sc.close();
    }
}
```
