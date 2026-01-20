# Bollywood Title Anagram

### Problem Statement

Raj works at a film production house in Mumbai. The marketing team often creates teaser posters with scrambled movie titles to build curiosity before the official reveal.

Given two strings `original` and `scrambled`, determine if `scrambled` is an anagram of `original`. An anagram uses all characters from the original string exactly once, just rearranged.

### Input Format

- The first line contains the string `original`.
- The second line contains the string `scrambled`.

### Output Format

- Print `true` if `scrambled` is an anagram of `original`, otherwise print `false`.

### Constraints

- `1 <= original.length, scrambled.length <= 5 * 10^4`
- Both strings consist of lowercase English letters only

### Test Cases

#### Test Case 1
**Input:**
```
anagram
nagaram
```
**Output:**
```
true
```
**Explanation:** Both strings contain: a(3), n(1), g(1), r(1), m(1). Valid anagram.

---

#### Test Case 2
**Input:**
```
rat
car
```
**Output:**
```
false
```
**Explanation:** "rat" has 't' but "car" has 'c'. Not an anagram.

---

#### Test Case 3
**Input:**
```
listen
silent
```
**Output:**
```
true
```
**Explanation:** Both contain the same characters rearranged.

---

#### Test Case 4
**Input:**
```
hello
world
```
**Output:**
```
false
```
**Explanation:** Completely different characters.

---

#### Test Case 5
**Input:**
```
a
a
```
**Output:**
```
true
```
**Explanation:** Single character, identical strings.

---

#### Test Case 6
**Input:**
```
ab
ba
```
**Output:**
```
true
```
**Explanation:** Simple two-character anagram.

---

#### Test Case 7
**Input:**
```
aacc
ccac
```
**Output:**
```
false
```
**Explanation:** "aacc" has a(2), c(2). "ccac" has c(3), a(1). Different frequencies.

---

### Solutions

#### Python

```python
class Solution:
    def isAnagram(self, original: str, scrambled: str) -> bool:
        # start your solution
        if len(original) != len(scrambled):
            return False
        
        freq = [0] * 26
        for i in range(len(original)):
            freq[ord(original[i]) - ord('a')] += 1
            freq[ord(scrambled[i]) - ord('a')] -= 1
        
        for count in freq:
            if count != 0:
                return False
        return True
        # end your solution


def main():
    original = input().strip()
    scrambled = input().strip()
    
    sol = Solution()
    result = sol.isAnagram(original, scrambled)
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
    bool isAnagram(string original, string scrambled) {
        // start your solution
        if (original.length() != scrambled.length()) {
            return false;
        }
        
        int freq[26] = {0};
        for (int i = 0; i < original.length(); i++) {
            freq[original[i] - 'a']++;
            freq[scrambled[i] - 'a']--;
        }
        
        for (int i = 0; i < 26; i++) {
            if (freq[i] != 0) {
                return false;
            }
        }
        return true;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string original, scrambled;
    cin >> original >> scrambled;
    
    Solution sol;
    cout << (sol.isAnagram(original, scrambled) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public boolean isAnagram(String original, String scrambled) {
        // start your solution
        if (original.length() != scrambled.length()) {
            return false;
        }
        
        int[] freq = new int[26];
        for (int i = 0; i < original.length(); i++) {
            freq[original.charAt(i) - 'a']++;
            freq[scrambled.charAt(i) - 'a']--;
        }
        
        for (int count : freq) {
            if (count != 0) {
                return false;
            }
        }
        return true;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String original = sc.nextLine().trim();
        String scrambled = sc.nextLine().trim();
        
        Solution sol = new Solution();
        System.out.println(sol.isAnagram(original, scrambled) ? "true" : "false");
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def isAnagram(self, original: str, scrambled: str) -> bool:
        # start your solution
        
        
        
        # end your solution


def main():
    original = input().strip()
    scrambled = input().strip()
    
    sol = Solution()
    result = sol.isAnagram(original, scrambled)
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
    bool isAnagram(string original, string scrambled) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string original, scrambled;
    cin >> original >> scrambled;
    
    Solution sol;
    cout << (sol.isAnagram(original, scrambled) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public boolean isAnagram(String original, String scrambled) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String original = sc.nextLine().trim();
        String scrambled = sc.nextLine().trim();
        
        Solution sol = new Solution();
        System.out.println(sol.isAnagram(original, scrambled) ? "true" : "false");
        
        sc.close();
    }
}
```
