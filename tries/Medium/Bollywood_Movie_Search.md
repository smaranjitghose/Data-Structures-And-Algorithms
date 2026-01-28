# Bollywood Movie Search

### Problem Statement

FilmiBaatein, a popular Indian movie database website, is building a search feature where users can find Bollywood movies even when they don't remember the exact title. Users can use `.` as a wildcard character that matches any single letter.

For example, if searching for "d..l" it could match "daal", "deal", "doll", etc. This helps users find movies like "D..g" matching "Dang", "Ding", "Dong", etc.

Design a data structure that supports:
- `addWord(word)`: Adds a movie title to the database
- `search(word)`: Returns `true` if any movie in the database matches the pattern. A `.` can match any single character.

### Input Format

- First line contains the number of operations `n`
- Next `n` lines each contain an operation: `addWord title` or `search pattern`

### Output Format

- For each `search` operation, print `true` or `false`
- `addWord` operations produce no output

### Constraints

- `1 <= n <= 10^4`
- `1 <= word.length <= 25`
- `word` in `addWord` consists of lowercase English letters
- `word` in `search` consists of lowercase English letters or `.`

### Test Cases

#### Test Case 1
**Input:**
```
8
addWord sholay
addWord deewar
addWord zanjeer
search sholay
search deewar
search .eewar
search sho...
search ......
```
**Output:**
```
true
true
true
true
true
```
**Explanation:** "sholay" and "deewar" exist. ".eewar" matches "deewar". "sho..." matches "sholay". "......" matches both 6-letter words.

---

#### Test Case 2
**Input:**
```
5
addWord ddlj
addWord kkhh
search d..j
search k..h
search ....
```
**Output:**
```
true
true
true
```
**Explanation:** "d..j" matches "ddlj", "k..h" matches "kkhh", "...." matches both.

---

#### Test Case 3
**Input:**
```
4
addWord lagaan
search lagaan
search l.....
search .......
```
**Output:**
```
true
true
false
```
**Explanation:** "lagaan" is 6 letters. "......." is 7 dots, doesn't match.

---

#### Test Case 4
**Input:**
```
3
addWord a
search .
search a
```
**Output:**
```
true
true
```
**Explanation:** Single character word matches single dot.

---

#### Test Case 5
**Input:**
```
4
addWord rang
addWord rann
search ra..
search r.n.
```
**Output:**
```
true
true
```
**Explanation:** Both patterns match "rang" and/or "rann".

---

#### Test Case 6
**Input:**
```
4
search gadar
addWord gadar
search gadar
search g....
```
**Output:**
```
false
true
true
```
**Explanation:** First search fails (not added yet), subsequent searches succeed.

---

#### Test Case 7
**Input:**
```
6
addWord ab
addWord abc
addWord abcd
search .b
search .bc
search ....
```
**Output:**
```
true
true
true
```
**Explanation:** ".b" matches "ab", ".bc" matches "abc", "...." matches "abcd".

---

### Solutions

#### Python
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False


class WordDictionary:
    def __init__(self):
        # start your solution
        self.root = TrieNode()

    def addWord(self, word: str) -> None:
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True

    def search(self, word: str) -> bool:
        return self._search_helper(word, 0, self.root)
    
    def _search_helper(self, word: str, index: int, node: TrieNode) -> bool:
        if index == len(word):
            return node.is_end
        
        char = word[index]
        
        if char == '.':
            for child in node.children.values():
                if self._search_helper(word, index + 1, child):
                    return True
            return False
        else:
            if char not in node.children:
                return False
            return self._search_helper(word, index + 1, node.children[char])
        # end your solution


def main():
    n = int(input())
    wd = WordDictionary()
    
    for _ in range(n):
        line = input().split()
        operation = line[0]
        argument = line[1]
        
        if operation == "addWord":
            wd.addWord(argument)
        elif operation == "search":
            print("true" if wd.search(argument) else "false")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <string>
#include <unordered_map>
using namespace std;

class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    bool isEnd;
    
    TrieNode() {
        isEnd = false;
    }
};

class WordDictionary {
private:
    TrieNode* root;
    
    bool searchHelper(const string& word, int index, TrieNode* node) {
        if (index == word.length()) {
            return node->isEnd;
        }
        
        char c = word[index];
        
        if (c == '.') {
            for (auto& [ch, child] : node->children) {
                if (searchHelper(word, index + 1, child)) {
                    return true;
                }
            }
            return false;
        } else {
            if (node->children.find(c) == node->children.end()) {
                return false;
            }
            return searchHelper(word, index + 1, node->children[c]);
        }
    }
    
public:
    WordDictionary() {
        // start your solution
        root = new TrieNode();
    }
    
    void addWord(string word) {
        TrieNode* node = root;
        for (char c : word) {
            if (node->children.find(c) == node->children.end()) {
                node->children[c] = new TrieNode();
            }
            node = node->children[c];
        }
        node->isEnd = true;
    }
    
    bool search(string word) {
        return searchHelper(word, 0, root);
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    WordDictionary wd;
    
    for (int i = 0; i < n; i++) {
        string operation, argument;
        cin >> operation >> argument;
        
        if (operation == "addWord") {
            wd.addWord(argument);
        } else if (operation == "search") {
            cout << (wd.search(argument) ? "true" : "false") << endl;
        }
    }
    
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

class WordDictionary {
    private TrieNode root;
    
    public WordDictionary() {
        // start your solution
        root = new TrieNode();
    }
    
    public void addWord(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            if (!node.children.containsKey(c)) {
                node.children.put(c, new TrieNode());
            }
            node = node.children.get(c);
        }
        node.isEnd = true;
    }
    
    public boolean search(String word) {
        return searchHelper(word, 0, root);
    }
    
    private boolean searchHelper(String word, int index, TrieNode node) {
        if (index == word.length()) {
            return node.isEnd;
        }
        
        char c = word.charAt(index);
        
        if (c == '.') {
            for (TrieNode child : node.children.values()) {
                if (searchHelper(word, index + 1, child)) {
                    return true;
                }
            }
            return false;
        } else {
            if (!node.children.containsKey(c)) {
                return false;
            }
            return searchHelper(word, index + 1, node.children.get(c));
        }
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        WordDictionary wd = new WordDictionary();
        
        for (int i = 0; i < n; i++) {
            String operation = sc.next();
            String argument = sc.next();
            
            if (operation.equals("addWord")) {
                wd.addWord(argument);
            } else if (operation.equals("search")) {
                System.out.println(wd.search(argument) ? "true" : "false");
            }
        }
        
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


class WordDictionary:
    def __init__(self):
        # start your solution
        pass

    def addWord(self, word: str) -> None:
        pass

    def search(self, word: str) -> bool:
        pass
        # end your solution


def main():
    n = int(input())
    wd = WordDictionary()
    
    for _ in range(n):
        line = input().split()
        operation = line[0]
        argument = line[1]
        
        if operation == "addWord":
            wd.addWord(argument)
        elif operation == "search":
            print("true" if wd.search(argument) else "false")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <string>
#include <unordered_map>
using namespace std;

class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    bool isEnd;
    
    TrieNode() {
        isEnd = false;
    }
};

class WordDictionary {
private:
    TrieNode* root;
    
public:
    WordDictionary() {
        // start your solution
        
    }
    
    void addWord(string word) {
        
    }
    
    bool search(string word) {
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    WordDictionary wd;
    
    for (int i = 0; i < n; i++) {
        string operation, argument;
        cin >> operation >> argument;
        
        if (operation == "addWord") {
            wd.addWord(argument);
        } else if (operation == "search") {
            cout << (wd.search(argument) ? "true" : "false") << endl;
        }
    }
    
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

class WordDictionary {
    private TrieNode root;
    
    public WordDictionary() {
        // start your solution
        
    }
    
    public void addWord(String word) {
        
    }
    
    public boolean search(String word) {
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        WordDictionary wd = new WordDictionary();
        
        for (int i = 0; i < n; i++) {
            String operation = sc.next();
            String argument = sc.next();
            
            if (operation.equals("addWord")) {
                wd.addWord(argument);
            } else if (operation.equals("search")) {
                System.out.println(wd.search(argument) ? "true" : "false");
            }
        }
        
        sc.close();
    }
}
```
