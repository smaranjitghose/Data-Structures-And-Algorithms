# Spice Box Mystery Ingredient

### Problem Statement

A famous chef in Chennai is teaching his apprentice to prepare a traditional spice box (masala dabba). The chef prepares a spice box with certain spices represented by lowercase letters, where each letter represents a unique spice. The apprentice creates a copy but secretly adds one extra spice to impress the chef.

Given two strings `s` (chef's spice box) and `t` (apprentice's spice box), where `t` is a shuffled version of `s` with one additional spice added at a random position, find and return the extra spice that was added.

### Input Format

- First line contains the string `s` (chef's spice box)
- Second line contains the string `t` (apprentice's spice box)

### Output Format

- A single character representing the extra spice added

### Constraints

- `0 <= s.length <= 1000`
- `t.length == s.length + 1`
- `s` and `t` consist of lowercase English letters

### Test Cases

#### Test Case 1
**Input:**
```
abcd
abcde
```
**Output:**
```
e
```
**Explanation:** 'e' is the extra spice added to the apprentice's box.

---

#### Test Case 2
**Input:**

a
```
**Output:**
```
a
```
**Explanation:** Chef's box is empty, apprentice added 'a'.

---

#### Test Case 3
**Input:**
```
aa
aaa
```
**Output:**
```
a
```
**Explanation:** One more 'a' was added.

---

#### Test Case 4
**Input:**
```
turmeric
mturericy
```
**Output:**
```
y
```
**Explanation:** 'y' is the additional character in the shuffled string.

---

#### Test Case 5
**Input:**
```
abcdefghijklmnopqrstuvwxyz
abcdefghijklmnopqrstuvwxyzz
```
**Output:**
```
z
```
**Explanation:** An extra 'z' was added.

---

#### Test Case 6
**Input:**
```
aabbcc
aabbccd
```
**Output:**
```
d
```
**Explanation:** 'd' is the new spice.

---

#### Test Case 7
**Input:**
```
xyz
xyza
```
**Output:**
```
a
```
**Explanation:** 'a' was added to the apprentice's box.

---

### Solutions

#### Python
```python
class Solution:
    def findTheDifference(self, s: str, t: str) -> str:
        # start your solution
        count = {}
        
        for char in s:
            count[char] = count.get(char, 0) + 1
        
        for char in t:
            if char not in count or count[char] == 0:
                return char
            count[char] -= 1
        
        return ''
        # end your solution


def main():
    s = input().strip()
    t = input().strip()
    
    sol = Solution()
    print(sol.findTheDifference(s, t))


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
    char findTheDifference(string s, string t) {
        // start your solution
        unordered_map<char, int> count;
        
        for (char c : s) {
            count[c]++;
        }
        
        for (char c : t) {
            if (count.find(c) == count.end() || count[c] == 0) {
                return c;
            }
            count[c]--;
        }
        
        return ' ';
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
    cout << sol.findTheDifference(s, t) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public char findTheDifference(String s, String t) {
        // start your solution
        Map<Character, Integer> count = new HashMap<>();
        
        for (char c : s.toCharArray()) {
            count.put(c, count.getOrDefault(c, 0) + 1);
        }
        
        for (char c : t.toCharArray()) {
            if (!count.containsKey(c) || count.get(c) == 0) {
                return c;
            }
            count.put(c, count.get(c) - 1);
        }
        
        return ' ';
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String s = sc.nextLine();
        String t = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.findTheDifference(s, t));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class Solution:
    def findTheDifference(self, s: str, t: str) -> str:
        # start your solution
        
        
        
        # end your solution


def main():
    s = input().strip()
    t = input().strip()
    
    sol = Solution()
    print(sol.findTheDifference(s, t))


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
    char findTheDifference(string s, string t) {
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
    cout << sol.findTheDifference(s, t) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public char findTheDifference(String s, String t) {
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
        System.out.println(sol.findTheDifference(s, t));
        
        sc.close();
    }
}
```