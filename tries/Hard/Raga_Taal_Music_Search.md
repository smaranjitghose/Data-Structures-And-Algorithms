# Raga-Taal Music Search

### Problem Statement

A Carnatic music academy in Chennai is building a digital raga (melodic framework) database. Musicians often search for ragas based on their arohanam (ascending scale pattern) prefix and avarohanam (descending scale pattern) suffix. For example, a musician might want to find all ragas that start with "sa-ri-ga" and end with "pa-da-ni".

Given a list of raga names, design a data structure that supports searching for ragas by both prefix AND suffix simultaneously. The search should return the index of the word in the original list that has the given prefix AND suffix. If multiple words match, return the largest index. If no word matches, return -1.

Implement the `WordFilter` class:
- `WordFilter(words)`: Initializes the object with the list of raga names
- `f(prefix, suffix)`: Returns the index of the word that has the given prefix and suffix. If multiple valid indices exist, return the largest. Return -1 if no word exists.

### Input Format

- First line contains the number of raga names `n`
- Second line contains `n` space-separated raga names
- Third line contains the number of queries `q`
- Next `q` lines each contain `prefix suffix`

### Output Format

- For each query, print the index (0-indexed) or -1

### Constraints

- `1 <= n <= 10^4`
- `1 <= words[i].length <= 7`
- `1 <= prefix.length, suffix.length <= 7`
- `words[i]`, `prefix`, and `suffix` consist of lowercase English letters only
- `1 <= q <= 10^4`

### Test Cases

#### Test Case 1
**Input:**
```
3
kalyani shankarabharanam mayamalavagowla
3
ka ani
sha nam
ma gowla
```
**Output:**
```
0
1
2
```
**Explanation:** "kalyani" starts with "ka" and ends with "ani". "shankarabharanam" starts with "sha" and ends with "nam". "mayamalavagowla" starts with "ma" and ends with "gowla".

---

#### Test Case 2
**Input:**
```
2
bhairavi bilahari
2
b i
bi ri
```
**Output:**
```
1
-1
```
**Explanation:** Both start with "b" and end with "i", return largest index 1. "bi...ri" - bilahari starts with "bi" but ends with "ri", so index 1.

---

#### Test Case 3
**Input:**
```
4
todi todi todi todi
1
to di
```
**Output:**
```
3
```
**Explanation:** All match, return largest index 3.

---

#### Test Case 4
**Input:**
```
3
mohanam hindolam hamsadhwani
2
ham ni
xyz abc
```
**Output:**
```
2
-1
```
**Explanation:** "hamsadhwani" matches. No word matches "xyz...abc".

---

#### Test Case 5
**Input:**
```
2
kamboji karaharapriya
2
ka ji
ka iya
```
**Output:**
```
0
1
```
**Explanation:** "kamboji" matches first query. "karaharapriya" matches second query.

---

#### Test Case 6
**Input:**
```
3
a ab abc
2
a a
a c
```
**Output:**
```
0
2
```
**Explanation:** "a" starts and ends with "a". "abc" starts with "a" and ends with "c".

---

#### Test Case 7
**Input:**
```
5
darbari durga desh devagandhari dhanyasi
2
d i
dar ri
```
**Output:**
```
4
0
```
**Explanation:** Multiple match "d...i" (darbari, dhanyasi), return largest 4. "darbari" matches "dar...ri".

---

### Solutions

#### Python
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.index = -1


class WordFilter:
    def __init__(self, words: list[str]):
        # start your solution
        self.root = TrieNode()
        
        for index, word in enumerate(words):
            # Create all combinations: suffix + '#' + word
            for i in range(len(word) + 1):
                combined = word[i:] + '#' + word
                node = self.root
                for char in combined:
                    if char not in node.children:
                        node.children[char] = TrieNode()
                    node = node.children[char]
                    node.index = index

    def f(self, prefix: str, suffix: str) -> int:
        search_key = suffix + '#' + prefix
        node = self.root
        
        for char in search_key:
            if char not in node.children:
                return -1
            node = node.children[char]
        
        return node.index
        # end your solution


def main():
    n = int(input())
    words = input().split()
    q = int(input())
    
    wf = WordFilter(words)
    
    for _ in range(q):
        line = input().split()
        prefix = line[0]
        suffix = line[1]
        print(wf.f(prefix, suffix))


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
    int index;
    
    TrieNode() {
        index = -1;
    }
};

class WordFilter {
private:
    TrieNode* root;
    
public:
    WordFilter(vector<string>& words) {
        // start your solution
        root = new TrieNode();
        
        for (int idx = 0; idx < words.size(); idx++) {
            string word = words[idx];
            // Create all combinations: suffix + '#' + word
            for (int i = 0; i <= word.length(); i++) {
                string combined = word.substr(i) + '#' + word;
                TrieNode* node = root;
                for (char c : combined) {
                    if (node->children.find(c) == node->children.end()) {
                        node->children[c] = new TrieNode();
                    }
                    node = node->children[c];
                    node->index = idx;
                }
            }
        }
    }
    
    int f(string prefix, string suffix) {
        string searchKey = suffix + '#' + prefix;
        TrieNode* node = root;
        
        for (char c : searchKey) {
            if (node->children.find(c) == node->children.end()) {
                return -1;
            }
            node = node->children[c];
        }
        
        return node->index;
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
    
    int q;
    cin >> q;
    
    WordFilter wf(words);
    
    for (int i = 0; i < q; i++) {
        string prefix, suffix;
        cin >> prefix >> suffix;
        cout << wf.f(prefix, suffix) << endl;
    }
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class TrieNode {
    Map<Character, TrieNode> children;
    int index;
    
    TrieNode() {
        children = new HashMap<>();
        index = -1;
    }
}

class WordFilter {
    private TrieNode root;
    
    public WordFilter(String[] words) {
        // start your solution
        root = new TrieNode();
        
        for (int idx = 0; idx < words.length; idx++) {
            String word = words[idx];
            // Create all combinations: suffix + '#' + word
            for (int i = 0; i <= word.length(); i++) {
                String combined = word.substring(i) + '#' + word;
                TrieNode node = root;
                for (char c : combined.toCharArray()) {
                    if (!node.children.containsKey(c)) {
                        node.children.put(c, new TrieNode());
                    }
                    node = node.children.get(c);
                    node.index = idx;
                }
            }
        }
    }
    
    public int f(String prefix, String suffix) {
        String searchKey = suffix + '#' + prefix;
        TrieNode node = root;
        
        for (char c : searchKey.toCharArray()) {
            if (!node.children.containsKey(c)) {
                return -1;
            }
            node = node.children.get(c);
        }
        
        return node.index;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        sc.nextLine();
        String[] words = sc.nextLine().split(" ");
        int q = sc.nextInt();
        
        WordFilter wf = new WordFilter(words);
        
        for (int i = 0; i < q; i++) {
            String prefix = sc.next();
            String suffix = sc.next();
            System.out.println(wf.f(prefix, suffix));
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
        self.index = -1


class WordFilter:
    def __init__(self, words: list[str]):
        # start your solution
        pass

    def f(self, prefix: str, suffix: str) -> int:
        pass
        # end your solution


def main():
    n = int(input())
    words = input().split()
    q = int(input())
    
    wf = WordFilter(words)
    
    for _ in range(q):
        line = input().split()
        prefix = line[0]
        suffix = line[1]
        print(wf.f(prefix, suffix))


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
    int index;
    
    TrieNode() {
        index = -1;
    }
};

class WordFilter {
private:
    TrieNode* root;
    
public:
    WordFilter(vector<string>& words) {
        // start your solution
        
    }
    
    int f(string prefix, string suffix) {
        
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
    
    int q;
    cin >> q;
    
    WordFilter wf(words);
    
    for (int i = 0; i < q; i++) {
        string prefix, suffix;
        cin >> prefix >> suffix;
        cout << wf.f(prefix, suffix) << endl;
    }
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class TrieNode {
    Map<Character, TrieNode> children;
    int index;
    
    TrieNode() {
        children = new HashMap<>();
        index = -1;
    }
}

class WordFilter {
    private TrieNode root;
    
    public WordFilter(String[] words) {
        // start your solution
        
    }
    
    public int f(String prefix, String suffix) {
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        sc.nextLine();
        String[] words = sc.nextLine().split(" ");
        int q = sc.nextInt();
        
        WordFilter wf = new WordFilter(words);
        
        for (int i = 0; i < q; i++) {
            String prefix = sc.next();
            String suffix = sc.next();
            System.out.println(wf.f(prefix, suffix));
        }
        
        sc.close();
    }
}
```
