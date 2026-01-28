# Ayurveda Medicine Catalog

### Problem Statement

Patanjali Ayurved in Haridwar is building a digital catalog system for their extensive range of Ayurvedic medicines. The system needs to efficiently store medicine names and support quick lookups for both exact matches and prefix-based searches (useful when pharmacists type partial names).

Implement a `Trie` data structure that supports the following operations:

- `Trie()`: Initializes the trie object
- `insert(word)`: Inserts the medicine name `word` into the trie
- `search(word)`: Returns `true` if the exact medicine name `word` exists in the trie, `false` otherwise
- `startsWith(prefix)`: Returns `true` if any medicine name in the trie starts with the given `prefix`, `false` otherwise

### Input Format

- First line contains the number of operations `n`
- Next `n` lines each contain an operation in format: `operation_name argument`
  - Operations: `insert`, `search`, `startsWith`

### Output Format

- For each `search` and `startsWith` operation, print `true` or `false` on a new line
- `insert` operations produce no output

### Constraints

- `1 <= n <= 3 * 10^4`
- `1 <= word.length, prefix.length <= 2000`
- `word` and `prefix` consist only of lowercase English letters

### Test Cases

#### Test Case 1
**Input:**
```
7
insert chyawanprash
insert ashwagandha
insert arjunarishta
search chyawanprash
search chyawan
startsWith chyawan
startsWith ash
```
**Output:**
```
true
false
true
true
```
**Explanation:** "chyawanprash" exists exactly. "chyawan" doesn't exist as complete word but exists as prefix.

---

#### Test Case 2
**Input:**
```
4
insert triphala
search triphala
search guggul
startsWith tri
```
**Output:**
```
true
false
true
```
**Explanation:** "triphala" exists, "guggul" was never inserted, "tri" is a valid prefix.

---

#### Test Case 3
**Input:**
```
3
search amla
startsWith a
insert amla
```
**Output:**
```
false
false
```
**Explanation:** Search and prefix check before any insert returns false.

---

#### Test Case 4
**Input:**
```
5
insert a
search a
startsWith a
startsWith ab
search ab
```
**Output:**
```
true
true
false
false
```
**Explanation:** Single character "a" is inserted. "ab" doesn't exist.

---

#### Test Case 5
**Input:**
```
6
insert brahmi
insert brahmivati
search brahmi
search brahmivati
startsWith brahmi
startsWith brahmiv
```
**Output:**
```
true
true
true
true
```
**Explanation:** Both complete words exist; both prefixes are valid.

---

#### Test Case 6
**Input:**
```
5
insert shatavari
insert shankhpushpi
insert shilajit
startsWith sha
startsWith shi
```
**Output:**
```
true
true
```
**Explanation:** "sha" matches shatavari and shankhpushpi; "shi" matches shilajit.

---

#### Test Case 7
**Input:**
```
4
insert guduchi
insert guduchi
search guduchi
startsWith guduchi
```
**Output:**
```
true
true
```
**Explanation:** Duplicate insert is allowed; word still exists once.

---

### Solutions

#### Python
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False


class Trie:
    def __init__(self):
        # start your solution
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True

    def search(self, word: str) -> bool:
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end

    def startsWith(self, prefix: str) -> bool:
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True
        # end your solution


def main():
    n = int(input())
    trie = Trie()
    
    for _ in range(n):
        line = input().split()
        operation = line[0]
        argument = line[1]
        
        if operation == "insert":
            trie.insert(argument)
        elif operation == "search":
            print("true" if trie.search(argument) else "false")
        elif operation == "startsWith":
            print("true" if trie.startsWith(argument) else "false")


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

class Trie {
private:
    TrieNode* root;
    
public:
    Trie() {
        // start your solution
        root = new TrieNode();
    }
    
    void insert(string word) {
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
        TrieNode* node = root;
        for (char c : word) {
            if (node->children.find(c) == node->children.end()) {
                return false;
            }
            node = node->children[c];
        }
        return node->isEnd;
    }
    
    bool startsWith(string prefix) {
        TrieNode* node = root;
        for (char c : prefix) {
            if (node->children.find(c) == node->children.end()) {
                return false;
            }
            node = node->children[c];
        }
        return true;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    Trie trie;
    
    for (int i = 0; i < n; i++) {
        string operation, argument;
        cin >> operation >> argument;
        
        if (operation == "insert") {
            trie.insert(argument);
        } else if (operation == "search") {
            cout << (trie.search(argument) ? "true" : "false") << endl;
        } else if (operation == "startsWith") {
            cout << (trie.startsWith(argument) ? "true" : "false") << endl;
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

class Trie {
    private TrieNode root;
    
    public Trie() {
        // start your solution
        root = new TrieNode();
    }
    
    public void insert(String word) {
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
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            if (!node.children.containsKey(c)) {
                return false;
            }
            node = node.children.get(c);
        }
        return node.isEnd;
    }
    
    public boolean startsWith(String prefix) {
        TrieNode node = root;
        for (char c : prefix.toCharArray()) {
            if (!node.children.containsKey(c)) {
                return false;
            }
            node = node.children.get(c);
        }
        return true;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        Trie trie = new Trie();
        
        for (int i = 0; i < n; i++) {
            String operation = sc.next();
            String argument = sc.next();
            
            if (operation.equals("insert")) {
                trie.insert(argument);
            } else if (operation.equals("search")) {
                System.out.println(trie.search(argument) ? "true" : "false");
            } else if (operation.equals("startsWith")) {
                System.out.println(trie.startsWith(argument) ? "true" : "false");
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


class Trie:
    def __init__(self):
        # start your solution
        pass

    def insert(self, word: str) -> None:
        pass

    def search(self, word: str) -> bool:
        pass

    def startsWith(self, prefix: str) -> bool:
        pass
        # end your solution


def main():
    n = int(input())
    trie = Trie()
    
    for _ in range(n):
        line = input().split()
        operation = line[0]
        argument = line[1]
        
        if operation == "insert":
            trie.insert(argument)
        elif operation == "search":
            print("true" if trie.search(argument) else "false")
        elif operation == "startsWith":
            print("true" if trie.startsWith(argument) else "false")


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

class Trie {
private:
    TrieNode* root;
    
public:
    Trie() {
        // start your solution
        
    }
    
    void insert(string word) {
        
    }
    
    bool search(string word) {
        
    }
    
    bool startsWith(string prefix) {
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    Trie trie;
    
    for (int i = 0; i < n; i++) {
        string operation, argument;
        cin >> operation >> argument;
        
        if (operation == "insert") {
            trie.insert(argument);
        } else if (operation == "search") {
            cout << (trie.search(argument) ? "true" : "false") << endl;
        } else if (operation == "startsWith") {
            cout << (trie.startsWith(argument) ? "true" : "false") << endl;
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

class Trie {
    private TrieNode root;
    
    public Trie() {
        // start your solution
        
    }
    
    public void insert(String word) {
        
    }
    
    public boolean search(String word) {
        
    }
    
    public boolean startsWith(String prefix) {
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        Trie trie = new Trie();
        
        for (int i = 0; i < n; i++) {
            String operation = sc.next();
            String argument = sc.next();
            
            if (operation.equals("insert")) {
                trie.insert(argument);
            } else if (operation.equals("search")) {
                System.out.println(trie.search(argument) ? "true" : "false");
            } else if (operation.equals("startsWith")) {
                System.out.println(trie.startsWith(argument) ? "true" : "false");
            }
        }
        
        sc.close();
    }
}
```
