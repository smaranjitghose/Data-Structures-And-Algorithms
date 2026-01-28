# Practo Doctor Search Autocomplete

### Problem Statement

Practo, India's leading healthcare platform, wants to build an intelligent doctor search autocomplete system. As users type their search query (symptoms, specializations, or doctor names), the system should suggest the top 3 most relevant previous searches.

The relevance is determined by:
1. First, by frequency (most searched queries appear first)
2. For queries with the same frequency, by lexicographical (alphabetical) order

The system should:
- Initialize with a set of historical search queries and their frequencies
- As the user types each character, return top 3 matching suggestions
- When the user types '#', save the current query and reset for a new search

Implement the `AutocompleteSystem` class:
- `AutocompleteSystem(sentences, times)`: Initializes with historical queries and their frequencies
- `input(c)`: Takes a character input. If `c == '#'`, save the query and return empty list. Otherwise, return top 3 suggestions.

### Input Format

- First line contains number of historical sentences `n`
- Second line contains `n` sentences separated by `|` (pipe)
- Third line contains `n` space-separated frequencies
- Fourth line contains number of input sequences `q`
- Next `q` lines each contain an input sequence (characters ending with `#`)

### Output Format

- For each character in input (except `#`), print the top 3 suggestions space-separated (or `none` if no suggestions)
- Print a blank line after each `#` (end of query)

### Constraints

- `1 <= n <= 100`
- `1 <= sentences[i].length <= 100`
- `1 <= times[i] <= 50`
- `c` is a lowercase letter, space, or `#`
- Each input sequence ends with `#`

### Test Cases

#### Test Case 1
**Input:**
```
4
cardiologist in mumbai|cardiologist in delhi|cancer specialist|cardiac surgeon
5 3 2 2
1
ca#
```
**Output:**
```
cancer specialist cardiac surgeon cardiologist in delhi
cardiologist in mumbai cardiologist in delhi cardiac surgeon

```
**Explanation:** After 'c': top 3 by frequency. After 'ca': filtered to "ca" prefix.

---

#### Test Case 2
**Input:**
```
3
dentist near me|dermatologist|diabetes doctor
4 3 2
1
d#
```
**Output:**
```
dentist near me dermatologist diabetes doctor

```
**Explanation:** All start with 'd', sorted by frequency then lexicographically.

---

#### Test Case 3
**Input:**
```
2
fever treatment|flu symptoms
2 2
1
f#
```
**Output:**
```
fever treatment flu symptoms

```
**Explanation:** Same frequency, sorted lexicographically.

---

#### Test Case 4
**Input:**
```
3
eye doctor|ent specialist|emergency hospital
3 3 3
1
e#
```
**Output:**
```
emergency hospital ent specialist eye doctor

```
**Explanation:** Same frequency, lexicographical order.

---

#### Test Case 5
**Input:**
```
2
pediatrician|physician
5 3
2
p#
p#
```
**Output:**
```
pediatrician physician

pediatrician physician p

```
**Explanation:** After first query, 'p' is added with frequency 1. Second query shows it.

---

#### Test Case 6
**Input:**
```
1
ortho doctor
1
1
xyz#
```
**Output:**
```
none
none
none

```
**Explanation:** No suggestions for 'x', 'y', 'z'. Query "xyz" saved.

---

#### Test Case 7
**Input:**
```
3
skin care|skin doctor|skin specialist
3 2 1
1
skin #
```
**Output:**
```
skin care skin doctor skin specialist
skin care skin doctor skin specialist
skin care skin doctor skin specialist
skin care skin doctor skin specialist
skin care skin doctor skin specialist

```
**Explanation:** As user types "skin ", suggestions narrow but all still match.

---

### Solutions

#### Python
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.sentences = {}


class AutocompleteSystem:
    def __init__(self, sentences: list[str], times: list[int]):
        # start your solution
        self.root = TrieNode()
        self.current_input = ""
        self.current_node = self.root
        self.dead = False
        
        for sentence, time in zip(sentences, times):
            self._add_sentence(sentence, time)
    
    def _add_sentence(self, sentence: str, time: int):
        node = self.root
        for char in sentence:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
            node.sentences[sentence] = node.sentences.get(sentence, 0) + time
    
    def _get_top3(self, node: TrieNode) -> list[str]:
        items = list(node.sentences.items())
        items.sort(key=lambda x: (-x[1], x[0]))
        return [item[0] for item in items[:3]]
    
    def input(self, c: str) -> list[str]:
        if c == '#':
            self._add_sentence(self.current_input, 1)
            self.current_input = ""
            self.current_node = self.root
            self.dead = False
            return []
        
        self.current_input += c
        
        if self.dead:
            return []
        
        if c not in self.current_node.children:
            self.dead = True
            return []
        
        self.current_node = self.current_node.children[c]
        return self._get_top3(self.current_node)
        # end your solution


def main():
    n = int(input())
    sentences = input().split('|')
    times = list(map(int, input().split()))
    q = int(input())
    
    acs = AutocompleteSystem(sentences, times)
    
    for _ in range(q):
        query = input()
        for c in query:
            result = acs.input(c)
            if c == '#':
                print()
            elif result:
                print(" ".join(result))
            else:
                print("none")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <unordered_map>
#include <algorithm>
#include <sstream>
using namespace std;

class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    unordered_map<string, int> sentences;
    
    TrieNode() {}
};

class AutocompleteSystem {
private:
    TrieNode* root;
    TrieNode* currentNode;
    string currentInput;
    bool dead;
    
    void addSentence(const string& sentence, int time) {
        TrieNode* node = root;
        for (char c : sentence) {
            if (node->children.find(c) == node->children.end()) {
                node->children[c] = new TrieNode();
            }
            node = node->children[c];
            node->sentences[sentence] += time;
        }
    }
    
    vector<string> getTop3(TrieNode* node) {
        vector<pair<string, int>> items(node->sentences.begin(), node->sentences.end());
        sort(items.begin(), items.end(), [](const auto& a, const auto& b) {
            if (a.second != b.second) return a.second > b.second;
            return a.first < b.first;
        });
        
        vector<string> result;
        for (int i = 0; i < min(3, (int)items.size()); i++) {
            result.push_back(items[i].first);
        }
        return result;
    }
    
public:
    AutocompleteSystem(vector<string>& sentences, vector<int>& times) {
        // start your solution
        root = new TrieNode();
        currentNode = root;
        currentInput = "";
        dead = false;
        
        for (int i = 0; i < sentences.size(); i++) {
            addSentence(sentences[i], times[i]);
        }
    }
    
    vector<string> input(char c) {
        if (c == '#') {
            addSentence(currentInput, 1);
            currentInput = "";
            currentNode = root;
            dead = false;
            return {};
        }
        
        currentInput += c;
        
        if (dead) {
            return {};
        }
        
        if (currentNode->children.find(c) == currentNode->children.end()) {
            dead = true;
            return {};
        }
        
        currentNode = currentNode->children[c];
        return getTop3(currentNode);
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
    
    vector<string> sentences;
    stringstream ss(line);
    string sentence;
    while (getline(ss, sentence, '|')) {
        sentences.push_back(sentence);
    }
    
    getline(cin, line);
    vector<int> times;
    stringstream ss2(line);
    int t;
    while (ss2 >> t) {
        times.push_back(t);
    }
    
    int q;
    cin >> q;
    cin.ignore();
    
    AutocompleteSystem acs(sentences, times);
    
    for (int i = 0; i < q; i++) {
        string query;
        getline(cin, query);
        
        for (char c : query) {
            vector<string> result = acs.input(c);
            if (c == '#') {
                cout << endl;
            } else if (result.empty()) {
                cout << "none" << endl;
            } else {
                for (int j = 0; j < result.size(); j++) {
                    if (j > 0) cout << " ";
                    cout << result[j];
                }
                cout << endl;
            }
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
    Map<String, Integer> sentences;
    
    TrieNode() {
        children = new HashMap<>();
        sentences = new HashMap<>();
    }
}

class AutocompleteSystem {
    private TrieNode root;
    private TrieNode currentNode;
    private StringBuilder currentInput;
    private boolean dead;
    
    public AutocompleteSystem(String[] sentences, int[] times) {
        // start your solution
        root = new TrieNode();
        currentNode = root;
        currentInput = new StringBuilder();
        dead = false;
        
        for (int i = 0; i < sentences.length; i++) {
            addSentence(sentences[i], times[i]);
        }
    }
    
    private void addSentence(String sentence, int time) {
        TrieNode node = root;
        for (char c : sentence.toCharArray()) {
            if (!node.children.containsKey(c)) {
                node.children.put(c, new TrieNode());
            }
            node = node.children.get(c);
            node.sentences.put(sentence, node.sentences.getOrDefault(sentence, 0) + time);
        }
    }
    
    private List<String> getTop3(TrieNode node) {
        List<Map.Entry<String, Integer>> items = new ArrayList<>(node.sentences.entrySet());
        items.sort((a, b) -> {
            if (!a.getValue().equals(b.getValue())) {
                return b.getValue() - a.getValue();
            }
            return a.getKey().compareTo(b.getKey());
        });
        
        List<String> result = new ArrayList<>();
        for (int i = 0; i < Math.min(3, items.size()); i++) {
            result.add(items.get(i).getKey());
        }
        return result;
    }
    
    public List<String> input(char c) {
        if (c == '#') {
            addSentence(currentInput.toString(), 1);
            currentInput = new StringBuilder();
            currentNode = root;
            dead = false;
            return new ArrayList<>();
        }
        
        currentInput.append(c);
        
        if (dead) {
            return new ArrayList<>();
        }
        
        if (!currentNode.children.containsKey(c)) {
            dead = true;
            return new ArrayList<>();
        }
        
        currentNode = currentNode.children.get(c);
        return getTop3(currentNode);
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        sc.nextLine();
        String[] sentences = sc.nextLine().split("\\|");
        String[] timesStr = sc.nextLine().split(" ");
        int[] times = new int[timesStr.length];
        for (int i = 0; i < timesStr.length; i++) {
            times[i] = Integer.parseInt(timesStr[i]);
        }
        
        int q = sc.nextInt();
        sc.nextLine();
        
        AutocompleteSystem acs = new AutocompleteSystem(sentences, times);
        
        for (int i = 0; i < q; i++) {
            String query = sc.nextLine();
            
            for (char c : query.toCharArray()) {
                List<String> result = acs.input(c);
                if (c == '#') {
                    System.out.println();
                } else if (result.isEmpty()) {
                    System.out.println("none");
                } else {
                    System.out.println(String.join(" ", result));
                }
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
        self.sentences = {}


class AutocompleteSystem:
    def __init__(self, sentences: list[str], times: list[int]):
        # start your solution
        pass
    
    def input(self, c: str) -> list[str]:
        pass
        # end your solution


def main():
    n = int(input())
    sentences = input().split('|')
    times = list(map(int, input().split()))
    q = int(input())
    
    acs = AutocompleteSystem(sentences, times)
    
    for _ in range(q):
        query = input()
        for c in query:
            result = acs.input(c)
            if c == '#':
                print()
            elif result:
                print(" ".join(result))
            else:
                print("none")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <unordered_map>
#include <algorithm>
#include <sstream>
using namespace std;

class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    unordered_map<string, int> sentences;
    
    TrieNode() {}
};

class AutocompleteSystem {
private:
    TrieNode* root;
    TrieNode* currentNode;
    string currentInput;
    bool dead;
    
public:
    AutocompleteSystem(vector<string>& sentences, vector<int>& times) {
        // start your solution
        
    }
    
    vector<string> input(char c) {
        
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
    
    vector<string> sentences;
    stringstream ss(line);
    string sentence;
    while (getline(ss, sentence, '|')) {
        sentences.push_back(sentence);
    }
    
    getline(cin, line);
    vector<int> times;
    stringstream ss2(line);
    int t;
    while (ss2 >> t) {
        times.push_back(t);
    }
    
    int q;
    cin >> q;
    cin.ignore();
    
    AutocompleteSystem acs(sentences, times);
    
    for (int i = 0; i < q; i++) {
        string query;
        getline(cin, query);
        
        for (char c : query) {
            vector<string> result = acs.input(c);
            if (c == '#') {
                cout << endl;
            } else if (result.empty()) {
                cout << "none" << endl;
            } else {
                for (int j = 0; j < result.size(); j++) {
                    if (j > 0) cout << " ";
                    cout << result[j];
                }
                cout << endl;
            }
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
    Map<String, Integer> sentences;
    
    TrieNode() {
        children = new HashMap<>();
        sentences = new HashMap<>();
    }
}

class AutocompleteSystem {
    private TrieNode root;
    private TrieNode currentNode;
    private StringBuilder currentInput;
    private boolean dead;
    
    public AutocompleteSystem(String[] sentences, int[] times) {
        // start your solution
        
    }
    
    public List<String> input(char c) {
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        sc.nextLine();
        String[] sentences = sc.nextLine().split("\\|");
        String[] timesStr = sc.nextLine().split(" ");
        int[] times = new int[timesStr.length];
        for (int i = 0; i < timesStr.length; i++) {
            times[i] = Integer.parseInt(timesStr[i]);
        }
        
        int q = sc.nextInt();
        sc.nextLine();
        
        AutocompleteSystem acs = new AutocompleteSystem(sentences, times);
        
        for (int i = 0; i < q; i++) {
            String query = sc.nextLine();
            
            for (char c : query.toCharArray()) {
                List<String> result = acs.input(c);
                if (c == '#') {
                    System.out.println();
                } else if (result.isEmpty()) {
                    System.out.println("none");
                } else {
                    System.out.println(String.join(" ", result));
                }
            }
        }
        
        sc.close();
    }
}
```
