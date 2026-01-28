# IFSC Code Branch Finder

### Problem Statement

A fintech startup in Bengaluru is building a bank branch locator app. Indian banks use IFSC (Indian Financial System Code) codes to identify branches. Each IFSC code has 11 characters: the first 4 characters identify the bank (e.g., "SBIN" for SBI, "HDFC" for HDFC Bank), the 5th character is always "0", and the last 6 characters identify the specific branch.

The app wants to help users find common patterns among a set of IFSC codes to identify the bank and possibly the region. Given a list of IFSC codes, find the longest common prefix among all codes.

Given an array of IFSC codes as strings, return their longest common prefix. If there is no common prefix, return an empty string.

### Input Format

- First line contains the number of IFSC codes `n`
- Second line contains `n` space-separated IFSC codes

### Output Format

- A single string representing the longest common prefix (empty line if none)

### Constraints

- `1 <= n <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` consists of lowercase/uppercase English letters and digits only

### Test Cases

#### Test Case 1
**Input:**
```
3
SBIN0001234 SBIN0001567 SBIN0001890
```
**Output:**
```
SBIN0001
```
**Explanation:** All three codes share the prefix "SBIN0001" (same bank, same region cluster).

---

#### Test Case 2
**Input:**
```
3
HDFC0000001 ICIC0000001 SBIN0000001
```
**Output:**
```

```
**Explanation:** Different banks, no common prefix (empty string).

---

#### Test Case 3
**Input:**
```
1
PUNB0123456
```
**Output:**
```
PUNB0123456
```
**Explanation:** Single code, the entire string is the common prefix.

---

#### Test Case 4
**Input:**
```
4
UTIB0002001 UTIB0002002 UTIB0002003 UTIB0002004
```
**Output:**
```
UTIB000200
```
**Explanation:** All Axis Bank (UTIB) codes from the same branch cluster.

---

#### Test Case 5
**Input:**
```
3
KKBK0000001 KKBK0000002 KKBK0000003
```
**Output:**
```
KKBK000000
```
**Explanation:** Kotak Mahindra Bank codes with common prefix.

---

#### Test Case 6
**Input:**
```
2
BARB0MUMXXX BARB0DELXXX
```
**Output:**
```
BARB0
```
**Explanation:** Bank of Baroda Mumbai and Delhi branches share only bank identifier.

---

#### Test Case 7
**Input:**
```
3
CBIN0280001 CBIN0280002 CBIN0281001
```
**Output:**
```
CBIN028
```
**Explanation:** Central Bank codes from nearby regions.

---

### Solutions

#### Python
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.count = 0


class Solution:
    def longestCommonPrefix(self, strs: list[str]) -> str:
        # start your solution
        if not strs:
            return ""
        
        root = TrieNode()
        n = len(strs)
        
        for s in strs:
            node = root
            for char in s:
                if char not in node.children:
                    node.children[char] = TrieNode()
                node = node.children[char]
                node.count += 1
        
        prefix = []
        node = root
        
        while node.children:
            if len(node.children) != 1:
                break
            
            char = list(node.children.keys())[0]
            child = node.children[char]
            
            if child.count != n:
                break
            
            prefix.append(char)
            node = child
        
        return "".join(prefix)
        # end your solution


def main():
    n = int(input())
    strs = input().split()
    
    sol = Solution()
    print(sol.longestCommonPrefix(strs))


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
    int count;
    
    TrieNode() {
        count = 0;
    }
};

class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        // start your solution
        if (strs.empty()) {
            return "";
        }
        
        TrieNode* root = new TrieNode();
        int n = strs.size();
        
        for (const string& s : strs) {
            TrieNode* node = root;
            for (char c : s) {
                if (node->children.find(c) == node->children.end()) {
                    node->children[c] = new TrieNode();
                }
                node = node->children[c];
                node->count++;
            }
        }
        
        string prefix = "";
        TrieNode* node = root;
        
        while (!node->children.empty()) {
            if (node->children.size() != 1) {
                break;
            }
            
            char c = node->children.begin()->first;
            TrieNode* child = node->children[c];
            
            if (child->count != n) {
                break;
            }
            
            prefix += c;
            node = child;
        }
        
        return prefix;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<string> strs(n);
    for (int i = 0; i < n; i++) {
        cin >> strs[i];
    }
    
    Solution sol;
    cout << sol.longestCommonPrefix(strs) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class TrieNode {
    Map<Character, TrieNode> children;
    int count;
    
    TrieNode() {
        children = new HashMap<>();
        count = 0;
    }
}

class Solution {
    public String longestCommonPrefix(String[] strs) {
        // start your solution
        if (strs == null || strs.length == 0) {
            return "";
        }
        
        TrieNode root = new TrieNode();
        int n = strs.length;
        
        for (String s : strs) {
            TrieNode node = root;
            for (char c : s.toCharArray()) {
                if (!node.children.containsKey(c)) {
                    node.children.put(c, new TrieNode());
                }
                node = node.children.get(c);
                node.count++;
            }
        }
        
        StringBuilder prefix = new StringBuilder();
        TrieNode node = root;
        
        while (!node.children.isEmpty()) {
            if (node.children.size() != 1) {
                break;
            }
            
            char c = node.children.keySet().iterator().next();
            TrieNode child = node.children.get(c);
            
            if (child.count != n) {
                break;
            }
            
            prefix.append(c);
            node = child;
        }
        
        return prefix.toString();
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        String[] strs = new String[n];
        for (int i = 0; i < n; i++) {
            strs[i] = sc.next();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.longestCommonPrefix(strs));
        
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
        self.count = 0


class Solution:
    def longestCommonPrefix(self, strs: list[str]) -> str:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    strs = input().split()
    
    sol = Solution()
    print(sol.longestCommonPrefix(strs))


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
    int count;
    
    TrieNode() {
        count = 0;
    }
};

class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    vector<string> strs(n);
    for (int i = 0; i < n; i++) {
        cin >> strs[i];
    }
    
    Solution sol;
    cout << sol.longestCommonPrefix(strs) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class TrieNode {
    Map<Character, TrieNode> children;
    int count;
    
    TrieNode() {
        children = new HashMap<>();
        count = 0;
    }
}

class Solution {
    public String longestCommonPrefix(String[] strs) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        String[] strs = new String[n];
        for (int i = 0; i < n; i++) {
            strs[i] = sc.next();
        }
        
        Solution sol = new Solution();
        System.out.println(sol.longestCommonPrefix(strs));
        
        sc.close();
    }
}
```
