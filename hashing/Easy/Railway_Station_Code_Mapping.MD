# Railway Station Code Mapping

### Problem Statement

Indian Railways is upgrading their station code system. They want to verify if the old station codes can be mapped to new station codes consistently. Two code strings are considered "isomorphic" if each character in the old code can be replaced with a unique character to get the new code, while preserving the order and maintaining a one-to-one mapping.

Given two strings `s` (old codes) and `t` (new codes), determine if they are isomorphic. Two strings are isomorphic if the characters in `s` can be replaced to get `t`, where:
- All occurrences of a character must be replaced with the same character
- No two different characters can map to the same character
- A character can map to itself

### Input Format

- First line contains the string `s` (old code pattern)
- Second line contains the string `t` (new code pattern)

### Output Format

- Print `true` if the strings are isomorphic, `false` otherwise

### Constraints

- `1 <= s.length <= 5 * 10^4`
- `t.length == s.length`
- `s` and `t` consist of any valid ASCII characters

### Test Cases

#### Test Case 1
**Input:**
```
egg
add
```
**Output:**
```
true
```
**Explanation:** 'e' maps to 'a', 'g' maps to 'd'. Consistent mapping.

---

#### Test Case 2
**Input:**
```
foo
bar
```
**Output:**
```
false
```
**Explanation:** 'o' cannot map to both 'a' and 'r'.

---

#### Test Case 3
**Input:**
```
paper
title
```
**Output:**
```
true
```
**Explanation:** p→t, a→i, e→l, r→e. All mappings are consistent.

---

#### Test Case 4
**Input:**
```
badc
baba
```
**Output:**
```
false
```
**Explanation:** 'a' maps to 'a', 'd' maps to 'b', but 'c' cannot also map to 'a' (already used by 'a').

---

#### Test Case 5
**Input:**
```
abcdefghijklmnopqrstuvwxyz
bcdefghijklmnopqrstuvwxyza
```
**Output:**
```
true
```
**Explanation:** Each letter shifts to next, all mappings unique.

---

#### Test Case 6
**Input:**
```
a
a
```
**Output:**
```
true
```
**Explanation:** Single character maps to itself.

---

#### Test Case 7
**Input:**
```
ab
aa
```
**Output:**
```
false
```
**Explanation:** Both 'a' and 'b' cannot map to 'a'.

---

### Solutions

#### Python
```python
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        # start your solution
        if len(s) != len(t):
            return False
        
        s_to_t = {}
        t_to_s = {}
        
        for c1, c2 in zip(s, t):
            if c1 in s_to_t:
                if s_to_t[c1] != c2:
                    return False
            else:
                s_to_t[c1] = c2
            
            if c2 in t_to_s:
                if t_to_s[c2] != c1:
                    return False
            else:
                t_to_s[c2] = c1
        
        return True
        # end your solution


def main():
    s = input().strip()
    t = input().strip()
    
    sol = Solution()
    print("true" if sol.isIsomorphic(s, t) else "false")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <string>
#include <unordered_map>
using namespace std;

class Solution {
public:
    bool isIsomorphic(string s, string t) {
        // start your solution
        if (s.length() != t.length()) {
            return false;
        }
        
        unordered_map<char, char> sToT;
        unordered_map<char, char> tToS;
        
        for (int i = 0; i < s.length(); i++) {
            char c1 = s[i], c2 = t[i];
            
            if (sToT.count(c1)) {
                if (sToT[c1] != c2) return false;
            } else {
                sToT[c1] = c2;
            }
            
            if (tToS.count(c2)) {
                if (tToS[c2] != c1) return false;
            } else {
                tToS[c2] = c1;
            }
        }
        
        return true;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string s, t;
    getline(cin, s);
    getline(cin, t);
    
    Solution sol;
    cout << (sol.isIsomorphic(s, t) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public boolean isIsomorphic(String s, String t) {
        // start your solution
        if (s.length() != t.length()) {
            return false;
        }
        
        Map<Character, Character> sToT = new HashMap<>();
        Map<Character, Character> tToS = new HashMap<>();
        
        for (int i = 0; i < s.length(); i++) {
            char c1 = s.charAt(i), c2 = t.charAt(i);
            
            if (sToT.containsKey(c1)) {
                if (sToT.get(c1) != c2) return false;
            } else {
                sToT.put(c1, c2);
            }
            
            if (tToS.containsKey(c2)) {
                if (tToS.get(c2) != c1) return false;
            } else {
                tToS.put(c2, c1);
            }
        }
        
        return true;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String s = sc.nextLine();
        String t = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.isIsomorphic(s, t) ? "true" : "false");
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        # start your solution
        
        
        
        # end your solution


def main():
    s = input().strip()
    t = input().strip()
    
    sol = Solution()
    print("true" if sol.isIsomorphic(s, t) else "false")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <string>
#include <unordered_map>
using namespace std;

class Solution {
public:
    bool isIsomorphic(string s, string t) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string s, t;
    getline(cin, s);
    getline(cin, t);
    
    Solution sol;
    cout << (sol.isIsomorphic(s, t) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public boolean isIsomorphic(String s, String t) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String s = sc.nextLine();
        String t = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.isIsomorphic(s, t) ? "true" : "false");
        
        sc.close();
    }
}
```