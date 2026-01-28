# Tamil Sangam Literature Index

### Problem Statement

A linguistics professor at Madurai Kamaraj University is studying ancient Tamil Sangam literature. She has compiled a dictionary of Tamil root words and their extensions. A word is considered "buildable" if it can be constructed one letter at a time, where each intermediate prefix is also a valid word in the dictionary.

For example, if the dictionary contains "ka", "kal", "kali" - then "kali" is buildable because "k" → "ka" → "kal" → "kali" forms a valid chain (assuming all prefixes exist). However, if "kal" is missing, then "kali" is not buildable.

Given an array of words representing the dictionary, find the longest word that can be built one character at a time by other words in the dictionary. If there are multiple answers with the same length, return the one that is lexicographically smallest. If no buildable word exists, return an empty string.

### Input Format

- First line contains the number of words `n`
- Second line contains `n` space-separated words

### Output Format

- A single string representing the longest buildable word (empty string if none)

### Constraints

- `1 <= n <= 1000`
- `1 <= words[i].length <= 30`
- `words[i]` consists of lowercase English letters only

### Test Cases

#### Test Case 1
**Input:**
```
5
ka kal kali kalim kalima
```
**Output:**
```
kalima
```
**Explanation:** "kalima" can be built: k→ka→kal→kali→kalim→kalima (but we need "k" to exist, which doesn't, so let's reconsider). Actually we need each prefix. "ka" exists, "kal" exists, "kali" exists, "kalim" exists → "kalima" is buildable.

---

#### Test Case 2
**Input:**
```
6
a ap app appl apple apply
```
**Output:**
```
apple
```
**Explanation:** Both "apple" and "apply" have length 5 and are buildable. "apple" < "apply" lexicographically.

---

#### Test Case 3
**Input:**
```
4
tam tami tamil tamizh
```
**Output:**
```
tamil
```
**Explanation:** "tamil" is buildable: ta→tam→tami→tamil. "tamizh" is NOT buildable because "tamiz" doesn't exist.

---

#### Test Case 4
**Input:**
```
3
abc def ghi
```
**Output:**
```

```
**Explanation:** No word is buildable since single-character prefixes don't exist.

---

#### Test Case 5
**Input:**
```
7
a b c ab abc abcd abcde
```
**Output:**
```
abcde
```
**Explanation:** "abcde" is buildable: a→ab→abc→abcd→abcde.

---

#### Test Case 6
**Input:**
```
4
m ma mad mada
```
**Output:**
```
mada
```
**Explanation:** "mada" is buildable: m→ma→mad→mada.

---

#### Test Case 7
**Input:**
```
5
y yo yog yoga yogam
```
**Output:**
```
yogam
```
**Explanation:** "yogam" is buildable: y→yo→yog→yoga→yogam.

---

### Solutions

#### Python
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False


class Solution:
    def longestWord(self, words: list[str]) -> str:
        # start your solution
        root = TrieNode()
        
        for word in words:
            node = root
            for char in word:
                if char not in node.children:
                    node.children[char] = TrieNode()
                node = node.children[char]
            node.is_end = True
        
        result = ""
        
        for word in words:
            if len(word) > len(result) or (len(word) == len(result) and word < result):
                node = root
                buildable = True
                for i, char in enumerate(word):
                    node = node.children[char]
                    if not node.is_end:
                        buildable = False
                        break
                
                if buildable:
                    result = word
        
        return result
        # end your solution


def main():
    n = int(input())
    words = input().split()
    
    sol = Solution()
    print(sol.longestWord(words))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <unordered_map>
#include <sstream>
using namespace std;

class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    bool isEnd;
    
    TrieNode() {
        isEnd = false;
    }
};

class Solution {
public:
    string longestWord(vector<string>& words) {
        // start your solution
        TrieNode* root = new TrieNode();
        
        for (const string& word : words) {
            TrieNode* node = root;
            for (char c : word) {
                if (node->children.find(c) == node->children.end()) {
                    node->children[c] = new TrieNode();
                }
                node = node->children[c];
            }
            node->isEnd = true;
        }
        
        string result = "";
        
        for (const string& word : words) {
            if (word.length() > result.length() || 
                (word.length() == result.length() && word < result)) {
                TrieNode* node = root;
                bool buildable = true;
                
                for (char c : word) {
                    node = node->children[c];
                    if (!node->isEnd) {
                        buildable = false;
                        break;
                    }
                }
                
                if (buildable) {
                    result = word;
                }
            }
        }
        
        return result;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    cin.ignore();
    
    string line;
    getline(cin, line);
    
    vector<string> words;
    stringstream ss(line);
    string word;
    while (ss >> word) {
        words.push_back(word);
    }
    
    Solution sol;
    cout << sol.longestWord(words) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class TrieNode {
    Map<Character, TrieNode> children;
    boolean isEnd;
    
    TrieNode() {
        children = new HashMap<>();
        isEnd = false;
    }
}

class Solution {
    public String longestWord(String[] words) {
        // start your solution
        TrieNode root = new TrieNode();
        
        for (String word : words) {
            TrieNode node = root;
            for (char c : word.toCharArray()) {
                if (!node.children.containsKey(c)) {
                    node.children.put(c, new TrieNode());
                }
                node = node.children.get(c);
            }
            node.isEnd = true;
        }
        
        String result = "";
        
        for (String word : words) {
            if (word.length() > result.length() || 
                (word.length() == result.length() && word.compareTo(result) < 0)) {
                TrieNode node = root;
                boolean buildable = true;
                
                for (char c : word.toCharArray()) {
                    node = node.children.get(c);
                    if (!node.isEnd) {
                        buildable = false;
                        break;
                    }
                }
                
                if (buildable) {
                    result = word;
                }
            }
        }
        
        return result;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        sc.nextLine();
        String[] words = sc.nextLine().split(" ");
        
        Solution sol = new Solution();
        System.out.println(sol.longestWord(words));
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False


class Solution:
    def longestWord(self, words: list[str]) -> str:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    words = input().split()
    
    sol = Solution()
    print(sol.longestWord(words))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <unordered_map>
#include <sstream>
using namespace std;

class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    bool isEnd;
    
    TrieNode() {
        isEnd = false;
    }
};

class Solution {
public:
    string longestWord(vector<string>& words) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    cin.ignore();
    
    string line;
    getline(cin, line);
    
    vector<string> words;
    stringstream ss(line);
    string word;
    while (ss >> word) {
        words.push_back(word);
    }
    
    Solution sol;
    cout << sol.longestWord(words) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class TrieNode {
    Map<Character, TrieNode> children;
    boolean isEnd;
    
    TrieNode() {
        children = new HashMap<>();
        isEnd = false;
    }
}

class Solution {
    public String longestWord(String[] words) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        sc.nextLine();
        String[] words = sc.nextLine().split(" ");
        
        Solution sol = new Solution();
        System.out.println(sol.longestWord(words));
        
        sc.close();
    }
}
```
