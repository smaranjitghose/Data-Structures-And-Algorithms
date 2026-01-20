# Cricket Score Encoding

### Problem Statement

Venkat is a cricket statistician at the BCCI headquarters in Mumbai. He developed a sequence encoding system to compress match scores. The encoding works as follows:

- Start with "1"
- Each subsequent term describes the previous term using run-length encoding
- To describe a term, count consecutive identical digits and say "count followed by digit"

The sequence begins:
- Term 1: "1"
- Term 2: "11" (one 1)
- Term 3: "21" (two 1s)
- Term 4: "1211" (one 2, one 1)
- Term 5: "111221" (one 1, one 2, two 1s)

Given an integer `n`, return the nth term of this sequence.

### Input Format

- A single integer `n`.

### Output Format

- Print the nth term of the count-and-say sequence.

### Constraints

- `1 <= n <= 30`

### Test Cases

#### Test Case 1
**Input:**
```
1
```
**Output:**
```
1
```
**Explanation:** First term is the base case "1".

---

#### Test Case 2
**Input:**
```
2
```
**Output:**
```
11
```
**Explanation:** Describe term 1 ("1"): one 1 → "11".

---

#### Test Case 3
**Input:**
```
3
```
**Output:**
```
21
```
**Explanation:** Describe term 2 ("11"): two 1s → "21".

---

#### Test Case 4
**Input:**
```
4
```
**Output:**
```
1211
```
**Explanation:** Describe term 3 ("21"): one 2, one 1 → "1211".

---

#### Test Case 5
**Input:**
```
5
```
**Output:**
```
111221
```
**Explanation:** Describe term 4 ("1211"): one 1, one 2, two 1s → "111221".

---

#### Test Case 6
**Input:**
```
6
```
**Output:**
```
312211
```
**Explanation:** Describe term 5 ("111221"): three 1s, two 2s, one 1 → "312211".

---

#### Test Case 7
**Input:**
```
10
```
**Output:**
```
13211311123113112211
```
**Explanation:** Building up from term 1 through 9, term 10 is "13211311123113112211".

---

### Solutions

#### Python

```python
class Solution:
    def encodeScore(self, n: int) -> str:
        # start your solution
        if n == 1:
            return "1"
        
        prev = "1"
        for _ in range(n - 1):
            curr = ""
            i = 0
            while i < len(prev):
                digit = prev[i]
                count = 0
                while i < len(prev) and prev[i] == digit:
                    count += 1
                    i += 1
                curr += str(count) + digit
            prev = curr
        
        return prev
        # end your solution


def main():
    n = int(input())
    
    sol = Solution()
    result = sol.encodeScore(n)
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
    string encodeScore(int n) {
        // start your solution
        if (n == 1) return "1";
        
        string prev = "1";
        for (int j = 1; j < n; j++) {
            string curr = "";
            int i = 0;
            while (i < prev.length()) {
                char digit = prev[i];
                int count = 0;
                while (i < prev.length() && prev[i] == digit) {
                    count++;
                    i++;
                }
                curr += to_string(count) + digit;
            }
            prev = curr;
        }
        
        return prev;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    Solution sol;
    cout << sol.encodeScore(n) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public String encodeScore(int n) {
        // start your solution
        if (n == 1) return "1";
        
        String prev = "1";
        for (int j = 1; j < n; j++) {
            StringBuilder curr = new StringBuilder();
            int i = 0;
            while (i < prev.length()) {
                char digit = prev.charAt(i);
                int count = 0;
                while (i < prev.length() && prev.charAt(i) == digit) {
                    count++;
                    i++;
                }
                curr.append(count).append(digit);
            }
            prev = curr.toString();
        }
        
        return prev;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.encodeScore(n));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def encodeScore(self, n: int) -> str:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    
    sol = Solution()
    result = sol.encodeScore(n)
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
    string encodeScore(int n) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    Solution sol;
    cout << sol.encodeScore(n) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public String encodeScore(int n) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        
        Solution sol = new Solution();
        System.out.println(sol.encodeScore(n));
        
        sc.close();
    }
}
```
