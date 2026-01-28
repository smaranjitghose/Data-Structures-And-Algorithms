# India Post Pincode Revenue Calculator

### Problem Statement

India Post is analyzing delivery revenue across different regions. Each pincode (6-digit postal code) has an associated revenue value. The management wants to calculate the total revenue for all pincodes that share a common prefix.

For example, all pincodes starting with "560" belong to Bengaluru region. The system should quickly calculate the sum of revenue for all pincodes with a given prefix.

Implement a `MapSum` class:
- `MapSum()`: Initializes the object
- `insert(key, val)`: Inserts the key-value pair (pincode-revenue). If the pincode already exists, update its value.
- `sum(prefix)`: Returns the sum of all values whose keys start with the given prefix.

### Input Format

- First line contains the number of operations `n`
- Next `n` lines each contain an operation:
  - `insert key val` (key is a string, val is an integer)
  - `sum prefix`

### Output Format

- For each `sum` operation, print the total sum
- `insert` operations produce no output

### Constraints

- `1 <= n <= 50`
- `1 <= key.length, prefix.length <= 50`
- `key` and `prefix` consist of lowercase English letters
- `1 <= val <= 1000`

### Test Cases

#### Test Case 1
**Input:**
```
4
insert bangalore 1000
insert bengaluru 2000
sum beng
sum bang
```
**Output:**
```
2000
1000
```
**Explanation:** "beng" prefix matches "bengaluru" (2000). "bang" matches "bangalore" (1000).

---

#### Test Case 2
**Input:**
```
5
insert delhi 500
insert dehradun 300
insert daman 200
sum de
sum d
```
**Output:**
```
800
1000
```
**Explanation:** "de" matches delhi+dehradun=800. "d" matches all three=1000.

---

#### Test Case 3
**Input:**
```
4
insert mumbai 1000
insert mumbai 1500
sum mum
sum mumbai
```
**Output:**
```
1500
1500
```
**Explanation:** Update overwrites old value. Both queries match "mumbai".

---

#### Test Case 4
**Input:**
```
3
insert kolkata 400
sum kol
sum xyz
```
**Output:**
```
400
0
```
**Explanation:** "xyz" has no matching keys, sum is 0.

---

#### Test Case 5
**Input:**
```
6
insert chennai 600
insert chandigarh 700
insert cochin 500
sum ch
sum c
sum co
```
**Output:**
```
1300
1800
500
```
**Explanation:** "ch" matches chennai+chandigarh. "c" matches all. "co" matches cochin only.

---

#### Test Case 6
**Input:**
```
4
insert a 100
insert ab 200
insert abc 300
sum a
```
**Output:**
```
600
```
**Explanation:** All three keys start with "a".

---

#### Test Case 7
**Input:**
```
5
insert jaipur 250
insert jodhpur 350
insert jaisalmer 150
sum jai
sum jo
```
**Output:**
```
400
350
```
**Explanation:** "jai" matches jaipur+jaisalmer. "jo" matches jodhpur.

---

### Solutions

#### Python
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.value = 0


class MapSum:
    def __init__(self):
        # start your solution
        self.root = TrieNode()
        self.map = {}

    def insert(self, key: str, val: int) -> None:
        delta = val - self.map.get(key, 0)
        self.map[key] = val
        
        node = self.root
        for char in key:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
            node.value += delta

    def sum(self, prefix: str) -> int:
        node = self.root
        for char in prefix:
            if char not in node.children:
                return 0
            node = node.children[char]
        return node.value
        # end your solution


def main():
    n = int(input())
    ms = MapSum()
    
    for _ in range(n):
        line = input().split()
        operation = line[0]
        
        if operation == "insert":
            key = line[1]
            val = int(line[2])
            ms.insert(key, val)
        elif operation == "sum":
            prefix = line[1]
            print(ms.sum(prefix))


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
    int value;
    
    TrieNode() {
        value = 0;
    }
};

class MapSum {
private:
    TrieNode* root;
    unordered_map<string, int> map;
    
public:
    MapSum() {
        // start your solution
        root = new TrieNode();
    }
    
    void insert(string key, int val) {
        int delta = val - (map.count(key) ? map[key] : 0);
        map[key] = val;
        
        TrieNode* node = root;
        for (char c : key) {
            if (node->children.find(c) == node->children.end()) {
                node->children[c] = new TrieNode();
            }
            node = node->children[c];
            node->value += delta;
        }
    }
    
    int sum(string prefix) {
        TrieNode* node = root;
        for (char c : prefix) {
            if (node->children.find(c) == node->children.end()) {
                return 0;
            }
            node = node->children[c];
        }
        return node->value;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    MapSum ms;
    
    for (int i = 0; i < n; i++) {
        string operation;
        cin >> operation;
        
        if (operation == "insert") {
            string key;
            int val;
            cin >> key >> val;
            ms.insert(key, val);
        } else if (operation == "sum") {
            string prefix;
            cin >> prefix;
            cout << ms.sum(prefix) << endl;
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
    int value;
    
    TrieNode() {
        children = new HashMap<>();
        value = 0;
    }
}

class MapSum {
    private TrieNode root;
    private Map<String, Integer> map;
    
    public MapSum() {
        // start your solution
        root = new TrieNode();
        map = new HashMap<>();
    }
    
    public void insert(String key, int val) {
        int delta = val - map.getOrDefault(key, 0);
        map.put(key, val);
        
        TrieNode node = root;
        for (char c : key.toCharArray()) {
            if (!node.children.containsKey(c)) {
                node.children.put(c, new TrieNode());
            }
            node = node.children.get(c);
            node.value += delta;
        }
    }
    
    public int sum(String prefix) {
        TrieNode node = root;
        for (char c : prefix.toCharArray()) {
            if (!node.children.containsKey(c)) {
                return 0;
            }
            node = node.children.get(c);
        }
        return node.value;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        MapSum ms = new MapSum();
        
        for (int i = 0; i < n; i++) {
            String operation = sc.next();
            
            if (operation.equals("insert")) {
                String key = sc.next();
                int val = sc.nextInt();
                ms.insert(key, val);
            } else if (operation.equals("sum")) {
                String prefix = sc.next();
                System.out.println(ms.sum(prefix));
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
        self.value = 0


class MapSum:
    def __init__(self):
        # start your solution
        pass

    def insert(self, key: str, val: int) -> None:
        pass

    def sum(self, prefix: str) -> int:
        pass
        # end your solution


def main():
    n = int(input())
    ms = MapSum()
    
    for _ in range(n):
        line = input().split()
        operation = line[0]
        
        if operation == "insert":
            key = line[1]
            val = int(line[2])
            ms.insert(key, val)
        elif operation == "sum":
            prefix = line[1]
            print(ms.sum(prefix))


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
    int value;
    
    TrieNode() {
        value = 0;
    }
};

class MapSum {
private:
    TrieNode* root;
    unordered_map<string, int> map;
    
public:
    MapSum() {
        // start your solution
        
    }
    
    void insert(string key, int val) {
        
    }
    
    int sum(string prefix) {
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    MapSum ms;
    
    for (int i = 0; i < n; i++) {
        string operation;
        cin >> operation;
        
        if (operation == "insert") {
            string key;
            int val;
            cin >> key >> val;
            ms.insert(key, val);
        } else if (operation == "sum") {
            string prefix;
            cin >> prefix;
            cout << ms.sum(prefix) << endl;
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
    int value;
    
    TrieNode() {
        children = new HashMap<>();
        value = 0;
    }
}

class MapSum {
    private TrieNode root;
    private Map<String, Integer> map;
    
    public MapSum() {
        // start your solution
        
    }
    
    public void insert(String key, int val) {
        
    }
    
    public int sum(String prefix) {
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        MapSum ms = new MapSum();
        
        for (int i = 0; i < n; i++) {
            String operation = sc.next();
            
            if (operation.equals("insert")) {
                String key = sc.next();
                int val = sc.nextInt();
                ms.insert(key, val);
            } else if (operation.equals("sum")) {
                String prefix = sc.next();
                System.out.println(ms.sum(prefix));
            }
        }
        
        sc.close();
    }
}
```
