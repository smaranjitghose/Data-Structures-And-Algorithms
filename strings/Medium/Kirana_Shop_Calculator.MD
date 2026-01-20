# Kirana Shop Calculator

### Problem Statement

Ramesh runs a kirana (grocery) shop in Kanpur. His old calculator broke, and he needs to multiply large numbers for bulk orders. The numbers are too large to fit in standard integer types.

Given two non-negative integers `num1` and `num2` represented as strings, return their product as a string. You must not use any built-in BigInteger library or convert inputs directly to integers.

### Input Format

- The first line contains string `num1`.
- The second line contains string `num2`.

### Output Format

- Print the product of the two numbers as a string.

### Constraints

- `1 <= num1.length, num2.length <= 200`
- `num1` and `num2` consist of digits only
- Both numbers do not contain leading zeros, except "0" itself

### Test Cases

#### Test Case 1
**Input:**
```
2
3
```
**Output:**
```
6
```
**Explanation:** Simple single digit multiplication. 2 × 3 = 6.

---

#### Test Case 2
**Input:**
```
123
456
```
**Output:**
```
56088
```
**Explanation:** 123 × 456. Multiply digit by digit, handle carries. Result = 56088.

---

#### Test Case 3
**Input:**
```
0
12345
```
**Output:**
```
0
```
**Explanation:** Any number multiplied by 0 equals 0.

---

#### Test Case 4
**Input:**
```
999
999
```
**Output:**
```
998001
```
**Explanation:** 999 × 999 = 998001. Tests carry propagation across all digits.

---

#### Test Case 5
**Input:**
```
12
12
```
**Output:**
```
144
```
**Explanation:** 12 × 12 = 144. Simple two-digit multiplication.

---

#### Test Case 6
**Input:**
```
498828660196
840477629533
```
**Output:**
```
419254329864656431168468
```
**Explanation:** Large number multiplication. Cannot fit in 64-bit integer. String manipulation required.

---

#### Test Case 7
**Input:**
```
1
9999999999
```
**Output:**
```
9999999999
```
**Explanation:** Multiplying by 1 returns the same number.

---

### Solutions

#### Python

```python
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        # start your solution
        if num1 == "0" or num2 == "0":
            return "0"
        
        m, n = len(num1), len(num2)
        result = [0] * (m + n)
        
        for i in range(m - 1, -1, -1):
            for j in range(n - 1, -1, -1):
                mul = (ord(num1[i]) - ord('0')) * (ord(num2[j]) - ord('0'))
                p1, p2 = i + j, i + j + 1
                total = mul + result[p2]
                
                result[p2] = total % 10
                result[p1] += total // 10
        
        result_str = ''.join(map(str, result))
        return result_str.lstrip('0') or '0'
        # end your solution


def main():
    num1 = input().strip()
    num2 = input().strip()
    
    sol = Solution()
    result = sol.multiply(num1, num2)
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
    string multiply(string num1, string num2) {
        // start your solution
        if (num1 == "0" || num2 == "0") return "0";
        
        int m = num1.length(), n = num2.length();
        vector<int> result(m + n, 0);
        
        for (int i = m - 1; i >= 0; i--) {
            for (int j = n - 1; j >= 0; j--) {
                int mul = (num1[i] - '0') * (num2[j] - '0');
                int p1 = i + j, p2 = i + j + 1;
                int total = mul + result[p2];
                
                result[p2] = total % 10;
                result[p1] += total / 10;
            }
        }
        
        string str = "";
        for (int digit : result) {
            if (!(str.empty() && digit == 0)) {
                str += to_string(digit);
            }
        }
        
        return str.empty() ? "0" : str;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string num1, num2;
    cin >> num1 >> num2;
    
    Solution sol;
    cout << sol.multiply(num1, num2) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public String multiply(String num1, String num2) {
        // start your solution
        if (num1.equals("0") || num2.equals("0")) return "0";
        
        int m = num1.length(), n = num2.length();
        int[] result = new int[m + n];
        
        for (int i = m - 1; i >= 0; i--) {
            for (int j = n - 1; j >= 0; j--) {
                int mul = (num1.charAt(i) - '0') * (num2.charAt(j) - '0');
                int p1 = i + j, p2 = i + j + 1;
                int total = mul + result[p2];
                
                result[p2] = total % 10;
                result[p1] += total / 10;
            }
        }
        
        StringBuilder sb = new StringBuilder();
        for (int digit : result) {
            if (!(sb.length() == 0 && digit == 0)) {
                sb.append(digit);
            }
        }
        
        return sb.length() == 0 ? "0" : sb.toString();
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String num1 = sc.nextLine().trim();
        String num2 = sc.nextLine().trim();
        
        Solution sol = new Solution();
        System.out.println(sol.multiply(num1, num2));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        # start your solution
        
        
        
        # end your solution


def main():
    num1 = input().strip()
    num2 = input().strip()
    
    sol = Solution()
    result = sol.multiply(num1, num2)
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
    string multiply(string num1, string num2) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string num1, num2;
    cin >> num1 >> num2;
    
    Solution sol;
    cout << sol.multiply(num1, num2) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public String multiply(String num1, String num2) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String num1 = sc.nextLine().trim();
        String num2 = sc.nextLine().trim();
        
        Solution sol = new Solution();
        System.out.println(sol.multiply(num1, num2));
        
        sc.close();
    }
}
```
