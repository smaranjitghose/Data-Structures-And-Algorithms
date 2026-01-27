# Newspaper Cutout Message

### Problem Statement

A Bollywood film producer in Mumbai is creating a mystery thriller where the villain sends anonymous messages by cutting out letters from newspapers. The villain has access to a single newspaper page and wants to create a specific threatening message.

Given two strings: `ransomNote` (the message to create) and `magazine` (the available letters from the newspaper), determine if the ransom note can be constructed using the letters from the magazine. Each letter in the magazine can only be used once.

### Input Format

- First line contains the string `ransomNote` (message to create)
- Second line contains the string `magazine` (available letters)

### Output Format

- Print `true` if the ransom note can be constructed, `false` otherwise

### Constraints

- `1 <= ransomNote.length, magazine.length <= 10^5`
- `ransomNote` and `magazine` consist of lowercase English letters

### Test Cases

#### Test Case 1
**Input:**
```
a
b
```
**Output:**
```
false
```
**Explanation:** 'a' is not available in the magazine.

---

#### Test Case 2
**Input:**
```
aa
ab
```
**Output:**
```
false
```
**Explanation:** Need two 'a's but only one is available.

---

#### Test Case 3
**Input:**
```
aa
aab
```
**Output:**
```
true
```
**Explanation:** Two 'a's are available in the magazine.

---

#### Test Case 4
**Input:**
```
paisa
paisabahuthai
```
**Output:**
```
true
```
**Explanation:** All letters for "paisa" are available.

---

#### Test Case 5
**Input:**
```
mumbai
bombay
```
**Output:**
```
false
```
**Explanation:** 'u' and 'i' are not in "bombay".

---

#### Test Case 6
**Input:**
```
aaaaaa
aaaaaab
```
**Output:**
```
true
```
**Explanation:** Six 'a's needed, seven available.

---

#### Test Case 7
**Input:**
```
xyz
xyzxyzxyz
```
**Output:**
```
true
```
**Explanation:** All letters available with extras.

---

### Solutions

#### Python
```python
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        # start your solution
        char_count = {}
        
        for char in magazine:
            char_count[char] = char_count.get(char, 0) + 1
        
        for char in ransomNote:
            if char not in char_count or char_count[char] == 0:
                return False
            char_count[char] -= 1
        
        return True
        # end your solution


def main():
    ransomNote = input().strip()
    magazine = input().strip()
    
    sol = Solution()
    print("true" if sol.canConstruct(ransomNote, magazine) else "false")


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
    bool canConstruct(string ransomNote, string magazine) {
        // start your solution
        unordered_map<char, int> charCount;
        
        for (char c : magazine) {
            charCount[c]++;
        }
        
        for (char c : ransomNote) {
            if (charCount.find(c) == charCount.end() || charCount[c] == 0) {
                return false;
            }
            charCount[c]--;
        }
        
        return true;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string ransomNote, magazine;
    getline(cin, ransomNote);
    getline(cin, magazine);
    
    Solution sol;
    cout << (sol.canConstruct(ransomNote, magazine) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        // start your solution
        Map<Character, Integer> charCount = new HashMap<>();
        
        for (char c : magazine.toCharArray()) {
            charCount.put(c, charCount.getOrDefault(c, 0) + 1);
        }
        
        for (char c : ransomNote.toCharArray()) {
            if (!charCount.containsKey(c) || charCount.get(c) == 0) {
                return false;
            }
            charCount.put(c, charCount.get(c) - 1);
        }
        
        return true;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String ransomNote = sc.nextLine();
        String magazine = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.canConstruct(ransomNote, magazine) ? "true" : "false");
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        # start your solution
        
        
        
        # end your solution


def main():
    ransomNote = input().strip()
    magazine = input().strip()
    
    sol = Solution()
    print("true" if sol.canConstruct(ransomNote, magazine) else "false")


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
    bool canConstruct(string ransomNote, string magazine) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string ransomNote, magazine;
    getline(cin, ransomNote);
    getline(cin, magazine);
    
    Solution sol;
    cout << (sol.canConstruct(ransomNote, magazine) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String ransomNote = sc.nextLine();
        String magazine = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.canConstruct(ransomNote, magazine) ? "true" : "false");
        
        sc.close();
    }
}
```