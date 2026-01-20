# Unique Coach Code

### Problem Statement

Priya works at the Indian Railways booking counter in Howrah Junction, Kolkata. Each train coach has a code represented as a string of lowercase letters.

Given a string `coachCode`, find the index of the first non-repeating character. If no such character exists, return -1.

### Input Format

- A single line containing the string `coachCode`.

### Output Format

- Print a single integer — the index (0-indexed) of the first non-repeating character, or -1 if none exists.

### Constraints

- `1 <= coachCode.length <= 10^5`
- `coachCode` consists of only lowercase English letters

### Test Cases

#### Test Case 1
**Input:**
```
rajdhani
```
**Output:**
```
0
```
**Explanation:** In coach code "rajdhani", 'r' at index 0 is the first character that appears only once.

---

#### Test Case 2
**Input:**
```
shatabdi
```
**Output:**
```
0
```
**Explanation:** In coach code "shatabdi", 's' at index 0 is the first unique character.

---

#### Test Case 3
**Input:**
```
aaccbbdd
```
**Output:**
```
-1
```
**Explanation:** All characters in this coach code repeat, no unique character exists.

---

#### Test Case 4
**Input:**
```
s
```
**Output:**
```
0
```
**Explanation:** Single character coach code is always unique.

---

#### Test Case 5
**Input:**
```
sleeperss
```
**Output:**
```
2
```
**Explanation:** 's' repeats, 'l' at index 2 is the first unique character in this coach code.

---

#### Test Case 6
**Input:**
```
acacacac
```
**Output:**
```
-1
```
**Explanation:** Only 'a' and 'c' present in coach code, both repeat.

---

#### Test Case 7
**Input:**
```
gaaborat
```
**Output:**
```
2
```
**Explanation:** 'g' and 'a' repeat in coach code "gaaborat". 'b' at index 2 is the first unique character.

---

### Solutions

#### Python

```python
class Solution:
    def firstUniqueChar(self, coachCode: str) -> int:
        # start your solution
        freq = [0] * 26
        for char in coachCode:
            freq[ord(char) - ord('a')] += 1
        
        for i, char in enumerate(coachCode):
            if freq[ord(char) - ord('a')] == 1:
                return i
        return -1
        # end your solution


def main():
    coachCode = input().strip()
    
    sol = Solution()
    result = sol.firstUniqueChar(coachCode)
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
    int firstUniqueChar(string coachCode) {
        // start your solution
        int freq[26] = {0};
        for (char c : coachCode) {
            freq[c - 'a']++;
        }
        
        for (int i = 0; i < coachCode.length(); i++) {
            if (freq[coachCode[i] - 'a'] == 1) {
                return i;
            }
        }
        return -1;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string coachCode;
    cin >> coachCode;
    
    Solution sol;
    cout << sol.firstUniqueChar(coachCode) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int firstUniqueChar(String coachCode) {
        // start your solution
        int[] freq = new int[26];
        for (char c : coachCode.toCharArray()) {
            freq[c - 'a']++;
        }
        
        for (int i = 0; i < coachCode.length(); i++) {
            if (freq[coachCode.charAt(i) - 'a'] == 1) {
                return i;
            }
        }
        return -1;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String coachCode = sc.nextLine().trim();
        
        Solution sol = new Solution();
        System.out.println(sol.firstUniqueChar(coachCode));
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def firstUniqueChar(self, coachCode: str) -> int:
        # start your solution
        
        
        
        # end your solution


def main():
    coachCode = input().strip()
    
    sol = Solution()
    result = sol.firstUniqueChar(coachCode)
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
    int firstUniqueChar(string coachCode) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string coachCode;
    cin >> coachCode;
    
    Solution sol;
    cout << sol.firstUniqueChar(coachCode) << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public int firstUniqueChar(String coachCode) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String coachCode = sc.nextLine().trim();
        
        Solution sol = new Solution();
        System.out.println(sol.firstUniqueChar(coachCode));
        
        sc.close();
    }
}
```
