# ASI Monument Keyword Tagger

### Problem Statement

The Archaeological Survey of India (ASI) is digitizing descriptions of India's 3600+ protected monuments. They need an automated system to tag important keywords in monument descriptions. Given a description text and a list of heritage keywords, the system should find all positions where these keywords appear.

Given a text string and an array of keywords, return all index pairs `[i, j]` where `text[i...j]` (inclusive) is a word from the keywords list. Return the pairs sorted by their start index, and if two pairs have the same start index, sort by end index.

### Input Format

- First line contains the text string
- Second line contains the number of keywords `n`
- Third line contains `n` space-separated keywords

### Output Format

- Print each index pair on a new line as `start end`
- If no keywords found, print `none`

### Constraints

- `1 <= text.length <= 1000`
- `1 <= n <= 100`
- `1 <= words[i].length <= 50`
- `text` and `words[i]` consist of lowercase English letters

### Test Cases

#### Test Case 1
**Input:**
```
tajmahalagra
3
taj mahal agra
```
**Output:**
```
0 2
3 7
8 11
```
**Explanation:** "taj" at [0,2], "mahal" at [3,7], "agra" at [8,11].

---

#### Test Case 2
**Input:**
```
qutubminar
2
qutub minar
```
**Output:**
```
0 4
5 9
```
**Explanation:** "qutub" at [0,4], "minar" at [5,9].

---

#### Test Case 3
**Input:**
```
konaboridham
2
konark dham
```
**Output:**
```
none
```
**Explanation:** Neither "konark" nor "dham" appear in text (partial matches don't count).

---

#### Test Case 4
**Input:**
```
aaa
2
a aa
```
**Output:**
```
0 0
0 1
1 1
1 2
2 2
```
**Explanation:** "a" appears at indices 0, 1, 2. "aa" appears at [0,1] and [1,2].

---

#### Test Case 5
**Input:**
```
hampi
1
hampi
```
**Output:**
```
0 4
```
**Explanation:** Entire text matches the keyword.

---

#### Test Case 6
**Input:**
```
fortfort
1
fort
```
**Output:**
```
0 3
4 7
```
**Explanation:** "fort" appears twice.

---

#### Test Case 7
**Input:**
```
elephantacaves
3
elephant cave caves
```
**Output:**
```
0 7
9 13
```
**Explanation:** "elephant" at [0,7], "caves" at [9,13]. "cave" at [9,12] is also present.

---

### Solutions

#### Python
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False


class Solution:
    def indexPairs(self, text: str, words: list[str]) -> list[list[int]]:
        # start your solution
        root = TrieNode()
        
        for word in words:
            node = root
            for char in word:
                if char not in node.children:
                    node.children[char] = TrieNode()
                node = node.children[char]
            node.is_end = True
        
        result = []
        
        for i in range(len(text)):
            node = root
            for j in range(i, len(text)):
                char = text[j]
                if char not in node.children:
                    break
                node = node.children[char]
                if node.is_end:
                    result.append([i, j])
        
        return result
        # end your solution


def main():
    text = input().strip()
    n = int(input())
    words = input().split()
    
    sol = Solution()
    result = sol.indexPairs(text, words)
    
    if not result:
        print("none")
    else:
        for pair in result:
            print(pair[0], pair[1])


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
    vector<vector<int>> indexPairs(string text, vector<string>& words) {
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
        
        vector<vector<int>> result;
        
        for (int i = 0; i < text.length(); i++) {
            TrieNode* node = root;
            for (int j = i; j < text.length(); j++) {
                char c = text[j];
                if (node->children.find(c) == node->children.end()) {
                    break;
                }
                node = node->children[c];
                if (node->isEnd) {
                    result.push_back({i, j});
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
    
    string text;
    getline(cin, text);
    
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
    vector<vector<int>> result = sol.indexPairs(text, words);
    
    if (result.empty()) {
        cout << "none" << endl;
    } else {
        for (const auto& pair : result) {
            cout << pair[0] << " " << pair[1] << endl;
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

class Solution {
    public int[][] indexPairs(String text, String[] words) {
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
        
        List<int[]> result = new ArrayList<>();
        
        for (int i = 0; i < text.length(); i++) {
            TrieNode node = root;
            for (int j = i; j < text.length(); j++) {
                char c = text.charAt(j);
                if (!node.children.containsKey(c)) {
                    break;
                }
                node = node.children.get(c);
                if (node.isEnd) {
                    result.add(new int[]{i, j});
                }
            }
        }
        
        return result.toArray(new int[result.size()][]);
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String text = sc.nextLine();
        int n = sc.nextInt();
        sc.nextLine();
        String[] words = sc.nextLine().split(" ");
        
        Solution sol = new Solution();
        int[][] result = sol.indexPairs(text, words);
        
        if (result.length == 0) {
            System.out.println("none");
        } else {
            for (int[] pair : result) {
                System.out.println(pair[0] + " " + pair[1]);
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


class Solution:
    def indexPairs(self, text: str, words: list[str]) -> list[list[int]]:
        # start your solution
        
        
        
        # end your solution


def main():
    text = input().strip()
    n = int(input())
    words = input().split()
    
    sol = Solution()
    result = sol.indexPairs(text, words)
    
    if not result:
        print("none")
    else:
        for pair in result:
            print(pair[0], pair[1])


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
    vector<vector<int>> indexPairs(string text, vector<string>& words) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string text;
    getline(cin, text);
    
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
    vector<vector<int>> result = sol.indexPairs(text, words);
    
    if (result.empty()) {
        cout << "none" << endl;
    } else {
        for (const auto& pair : result) {
            cout << pair[0] << " " << pair[1] << endl;
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

class Solution {
    public int[][] indexPairs(String text, String[] words) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String text = sc.nextLine();
        int n = sc.nextInt();
        sc.nextLine();
        String[] words = sc.nextLine().split(" ");
        
        Solution sol = new Solution();
        int[][] result = sol.indexPairs(text, words);
        
        if (result.length == 0) {
            System.out.println("none");
        } else {
            for (int[] pair : result) {
                System.out.println(pair[0] + " " + pair[1]);
            }
        }
        
        sc.close();
    }
}
```
