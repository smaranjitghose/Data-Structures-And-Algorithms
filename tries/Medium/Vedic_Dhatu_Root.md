# Vedic Dhatu Root Replacer

### Problem Statement

A Sanskrit professor at Banaras Hindu University (BHU) is developing a tool for students to understand word etymology. In Sanskrit grammar, most words are derived from root words called "Dhatu" (धातु). For example, "gamana" (going) is derived from the dhatu "gam" (to go).

The professor has compiled a dictionary of dhatus (root words). Given a sentence of derived words, the tool should replace each word with its shortest matching dhatu (root). If a word has multiple dhatus as prefixes, use the shortest one. If no dhatu matches, keep the original word.

Given a dictionary of dhatus and a sentence, replace each word in the sentence with the shortest matching dhatu prefix.

### Input Format

- First line contains the number of dhatus `n`
- Second line contains `n` space-separated dhatus
- Third line contains the sentence (space-separated words)

### Output Format

- The sentence with words replaced by their shortest matching dhatu

### Constraints

- `1 <= n <= 1000`
- `1 <= dictionary[i].length <= 100`
- `1 <= sentence.length <= 10^6`
- All strings consist of lowercase English letters
- Sentence words are separated by single spaces

### Test Cases

#### Test Case 1
**Input:**
```
3
gam path vid
gamanam pathikah vidyarthi
```
**Output:**
```
gam path vid
```
**Explanation:** "gamanam" starts with "gam", "pathikah" starts with "path", "vidyarthi" starts with "vid".

---

#### Test Case 2
**Input:**
```
4
kri bhu stha char
kriya bhumi sthana charitram
```
**Output:**
```
kri bhu stha char
```
**Explanation:** Each word is replaced with its dhatu root.

---

#### Test Case 3
**Input:**
```
2
a ab
absolutely abstract
```
**Output:**
```
a a
```
**Explanation:** Both words start with "a" (shortest dhatu), not "ab".

---

#### Test Case 4
**Input:**
```
3
cat bat rat
cattle battery rationale
```
**Output:**
```
cat bat rat
```
**Explanation:** Standard prefix replacement.

---

#### Test Case 5
**Input:**
```
2
dha man
dharma mantra moksha
```
**Output:**
```
dha man moksha
```
**Explanation:** "moksha" has no matching dhatu, kept as is.

---

#### Test Case 6
**Input:**
```
4
pra upa sam vi
pranamah upanishad samskritam vidhya
```
**Output:**
```
pra upa sam vi
```
**Explanation:** Common Sanskrit prefixes as dhatus.

---

#### Test Case 7
**Input:**
```
1
guru
gurukulam gurudakshina gurudev
```
**Output:**
```
guru guru guru
```
**Explanation:** All words share the same dhatu "guru".

---

### Solutions

#### Python
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.word = None


class Solution:
    def replaceWords(self, dictionary: list[str], sentence: str) -> str:
        # start your solution
        root = TrieNode()
        
        for word in dictionary:
            node = root
            for char in word:
                if char not in node.children:
                    node.children[char] = TrieNode()
                node = node.children[char]
            if node.word is None:
                node.word = word
        
        def find_root(word):
            node = root
            for char in word:
                if char not in node.children:
                    break
                node = node.children[char]
                if node.word is not None:
                    return node.word
            return word
        
        words = sentence.split()
        result = [find_root(word) for word in words]
        
        return " ".join(result)
        # end your solution


def main():
    n = int(input())
    dictionary = input().split()
    sentence = input().strip()
    
    sol = Solution()
    print(sol.replaceWords(dictionary, sentence))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <sstream>
#include <unordered_map>
using namespace std;

class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    string word;
    
    TrieNode() {
        word = "";
    }
};

class Solution {
public:
    string replaceWords(vector<string>& dictionary, string sentence) {
        // start your solution
        TrieNode* root = new TrieNode();
        
        for (const string& w : dictionary) {
            TrieNode* node = root;
            for (char c : w) {
                if (node->children.find(c) == node->children.end()) {
                    node->children[c] = new TrieNode();
                }
                node = node->children[c];
            }
            if (node->word.empty()) {
                node->word = w;
            }
        }
        
        auto findRoot = [&](const string& word) -> string {
            TrieNode* node = root;
            for (char c : word) {
                if (node->children.find(c) == node->children.end()) {
                    break;
                }
                node = node->children[c];
                if (!node->word.empty()) {
                    return node->word;
                }
            }
            return word;
        };
        
        stringstream ss(sentence);
        string word;
        string result = "";
        bool first = true;
        
        while (ss >> word) {
            if (!first) result += " ";
            result += findRoot(word);
            first = false;
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
    
    vector<string> dictionary;
    stringstream ss(line);
    string word;
    while (ss >> word) {
        dictionary.push_back(word);
    }
    
    string sentence;
    getline(cin, sentence);
    
    Solution sol;
    cout << sol.replaceWords(dictionary, sentence) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class TrieNode {
    Map<Character, TrieNode> children;
    String word;
    
    TrieNode() {
        children = new HashMap<>();
        word = null;
    }
}

class Solution {
    public String replaceWords(List<String> dictionary, String sentence) {
        // start your solution
        TrieNode root = new TrieNode();
        
        for (String w : dictionary) {
            TrieNode node = root;
            for (char c : w.toCharArray()) {
                if (!node.children.containsKey(c)) {
                    node.children.put(c, new TrieNode());
                }
                node = node.children.get(c);
            }
            if (node.word == null) {
                node.word = w;
            }
        }
        
        String[] words = sentence.split(" ");
        StringBuilder result = new StringBuilder();
        
        for (int i = 0; i < words.length; i++) {
            if (i > 0) result.append(" ");
            result.append(findRoot(root, words[i]));
        }
        
        return result.toString();
    }
    
    private String findRoot(TrieNode root, String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            if (!node.children.containsKey(c)) {
                break;
            }
            node = node.children.get(c);
            if (node.word != null) {
                return node.word;
            }
        }
        return word;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        sc.nextLine();
        String[] dictArr = sc.nextLine().split(" ");
        List<String> dictionary = Arrays.asList(dictArr);
        String sentence = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.replaceWords(dictionary, sentence));
        
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
        self.word = None


class Solution:
    def replaceWords(self, dictionary: list[str], sentence: str) -> str:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    dictionary = input().split()
    sentence = input().strip()
    
    sol = Solution()
    print(sol.replaceWords(dictionary, sentence))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <sstream>
#include <unordered_map>
using namespace std;

class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    string word;
    
    TrieNode() {
        word = "";
    }
};

class Solution {
public:
    string replaceWords(vector<string>& dictionary, string sentence) {
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
    
    vector<string> dictionary;
    stringstream ss(line);
    string word;
    while (ss >> word) {
        dictionary.push_back(word);
    }
    
    string sentence;
    getline(cin, sentence);
    
    Solution sol;
    cout << sol.replaceWords(dictionary, sentence) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class TrieNode {
    Map<Character, TrieNode> children;
    String word;
    
    TrieNode() {
        children = new HashMap<>();
        word = null;
    }
}

class Solution {
    public String replaceWords(List<String> dictionary, String sentence) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        sc.nextLine();
        String[] dictArr = sc.nextLine().split(" ");
        List<String> dictionary = Arrays.asList(dictArr);
        String sentence = sc.nextLine();
        
        Solution sol = new Solution();
        System.out.println(sol.replaceWords(dictionary, sentence));
        
        sc.close();
    }
}
```
