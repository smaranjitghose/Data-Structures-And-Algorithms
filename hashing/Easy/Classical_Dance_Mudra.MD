# Classical Dance Mudra Pattern

### Problem Statement

A Bharatanatyam dance teacher in Chennai is teaching her students about mudra (hand gesture) patterns. Each mudra is represented by a letter in a pattern string, and each actual mudra name is a word in a sequence. The teacher wants to verify if the sequence of mudra names follows the given pattern correctly.

Given a pattern string and a space-separated string of mudra names, determine if the names follow the same pattern. "Follow" means there is a bijection (one-to-one mapping) between each letter in the pattern and each word in the sequence.

### Input Format

- First line contains the pattern string (letters only)
- Second line contains space-separated mudra names

### Output Format

- Print `true` if the sequence follows the pattern, `false` otherwise

### Constraints

- `1 <= pattern.length <= 300`
- `pattern` contains only lowercase English letters
- `1 <= s.length <= 3000`
- `s` contains only lowercase English letters and spaces
- `s` does not contain leading or trailing spaces
- All words in `s` are separated by a single space

### Test Cases

#### Test Case 1
**Input:**
```
abba
anjali katakamukha katakamukha anjali
```
**Output:**
```
true
```
**Explanation:** a→anjali, b→katakamukha. Pattern matches perfectly.

---

#### Test Case 2
**Input:**
```
abba
anjali katakamukha katakamukha alapadma
```
**Output:**
```
false
```
**Explanation:** 'a' maps to both 'anjali' and 'alapadma', which is inconsistent.

---

#### Test Case 3
**Input:**
```
aaaa
pataka pataka pataka pataka
```
**Output:**
```
true
```
**Explanation:** All 'a's map to 'pataka'.

---

#### Test Case 4
**Input:**
```
abcd
mayura hamsa simha garuda
```
**Output:**
```
true
```
**Explanation:** Each letter maps to a unique mudra name.

---

#### Test Case 5
**Input:**
```
aabb
mrigashirsha mrigashirsha kapitha kapitha
```
**Output:**
```
true
```
**Explanation:** a→mrigashirsha, b→kapitha.

---

#### Test Case 6
**Input:**
```
ab
shikhara shikhara
```
**Output:**
```
false
```
**Explanation:** Pattern has 2 different letters but both words are same.

---

#### Test Case 7
**Input:**
```
abc
hamsasya hamsapaksha hamsasya
```
**Output:**
```
false
```
**Explanation:** 'a' and 'c' both map to 'hamsasya', violating bijection.

---

### Solutions

#### Python
```python
class Solution:
    def wordPattern(self, pattern: str, s: str) -> bool:
        # start your solution
        words = s.split()
        
        if len(pattern) != len(words):
            return False
        
        char_to_word = {}
        word_to_char = {}
        
        for char, word in zip(pattern, words):
            if char in char_to_word:
                if char_to_word[char] != word:
                    return False
            else:
                char_to_word[char] = word
            
            if word in word_to_char:
                if word_to_char[word] != char:
                    return False
            else:
                word_to_char[word] = char
        
        return True
        # end your solution


def main():
    pattern = input().strip()
    s = input().strip()
    
    sol = Solution()
    print("true" if sol.wordPattern(pattern, s) else "false")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <string>
#include <sstream>
#include <vector>
#include <unordered_map>
using namespace std;

class Solution {
public:
    bool wordPattern(string pattern, string s) {
        // start your solution
        vector<string> words;
        stringstream ss(s);
        string word;
        while (ss >> word) {
            words.push_back(word);
        }
        
        if (pattern.length() != words.size()) {
            return false;
        }
        
        unordered_map<char, string> charToWord;
        unordered_map<string, char> wordToChar;
        
        for (int i = 0; i < pattern.length(); i++) {
            char c = pattern[i];
            string w = words[i];
            
            if (charToWord.count(c)) {
                if (charToWord[c] != w) return false;
            } else {
                charToWord[c] = w;
            }
            
            if (wordToChar.count(w)) {
                if (wordToChar[w] != c) return false;
            } else {
                wordToChar[w] = c;
            }
        }
        
        return true;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string pattern, s;
    getline(cin, pattern);
    getline(cin, s);
    
    Solution sol;
    cout << (sol.wordPattern(pattern, s) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public boolean wordPattern(String pattern, String s) {
        // start your solution
        String[] words = s.split(" ");
        
        if (pattern.length() != words.length) {
            return false;
        }
        
        Map<Character, String> charToWord = new HashMap<>();
        Map<String, Character> wordToChar = new HashMap<>();
        
        for (int i = 0; i < pattern.length(); i++) {
            char c = pattern.charAt(i);
            String w = words[i];
            
            if (charToWord.containsKey(c)) {
                if (!charToWord.get(c).equals(w)) return false;
            } else {
                charToWord.put(c, w);
            }
            
            if (wordToChar.containsKey(w)) {
                if (wordToChar.get(w) != c) return false;
            } else {
                wordToChar.put(w, c);
            }
        }
        
        return true;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String pattern = sc.nextLine();
        String s = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.wordPattern(pattern, s) ? "true" : "false");
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class Solution:
    def wordPattern(self, pattern: str, s: str) -> bool:
        # start your solution
        
        
        
        # end your solution


def main():
    pattern = input().strip()
    s = input().strip()
    
    sol = Solution()
    print("true" if sol.wordPattern(pattern, s) else "false")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <string>
#include <sstream>
#include <vector>
#include <unordered_map>
using namespace std;

class Solution {
public:
    bool wordPattern(string pattern, string s) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string pattern, s;
    getline(cin, pattern);
    getline(cin, s);
    
    Solution sol;
    cout << (sol.wordPattern(pattern, s) ? "true" : "false") << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public boolean wordPattern(String pattern, String s) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String pattern = sc.nextLine();
        String s = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.wordPattern(pattern, s) ? "true" : "false");
        
        sc.close();
    }
}
```