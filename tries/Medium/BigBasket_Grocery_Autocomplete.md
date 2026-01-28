# BigBasket Grocery Autocomplete

### Problem Statement

BigBasket, India's leading online grocery store, is implementing a smart search autocomplete feature. As customers type in the search box, the system should suggest up to 3 matching products that start with the typed prefix. The suggestions should be sorted lexicographically (alphabetically).

For each character typed, the system returns the top 3 lexicographically smallest products that match the current prefix. If fewer than 3 products match, return all matching products.

Given an array of product names and a search word, return a list of lists containing the suggested products after each character of the search word is typed.

### Input Format

- First line contains the number of products `n`
- Second line contains `n` space-separated product names
- Third line contains the search word

### Output Format

- For each character typed, print up to 3 suggestions on a single line, space-separated
- If no suggestions, print `none`

### Constraints

- `1 <= n <= 1000`
- `1 <= products[i].length <= 100`
- `1 <= searchWord.length <= 100`
- All strings consist of lowercase English letters

### Test Cases

#### Test Case 1
**Input:**
```
5
atta achar amchur ajwain asafoetida
aat
```
**Output:**
```
achar ajwain amchur
aatta
none
```
**Explanation:** After 'a': top 3 starting with 'a'. After 'aa': only products starting with 'aa'. After 'aat': none match.

---

#### Test Case 2
**Input:**
```
6
dal dalia dhaniya dalchini dates dabeli
dal
```
**Output:**
```
dabeli dal dalchini
dal dalchini dalia
dal dalchini dalia
```
**Explanation:** "dal" prefix matches change as more letters are typed.

---

#### Test Case 3
**Input:**
```
4
rice rajma ragi rava
ra
```
**Output:**
```
ragi rajma rava
ragi rajma rava
```
**Explanation:** After 'r': ragi, rajma, rava (top 3). After 'ra': same products match.

---

#### Test Case 4
**Input:**
```
3
paneer palak poha
pa
```
**Output:**
```
palak paneer poha
palak paneer
```
**Explanation:** After 'p': all 3. After 'pa': only palak and paneer match.

---

#### Test Case 5
**Input:**
```
5
sugar salt sooji saunf safed
sug
```
**Output:**
```
safed salt saunf
sugar
sugar
```
**Explanation:** Suggestions narrow down as prefix gets specific.

---

#### Test Case 6
**Input:**
```
3
ghee ginger garlic
gh
```
**Output:**
```
garlic ghee ginger
ghee
```
**Explanation:** After 'g': all 3 sorted. After 'gh': only ghee.

---

#### Test Case 7
**Input:**
```
4
tea turmeric tamarind toor
t
```
**Output:**
```
tamarind tea toor
```
**Explanation:** Single character prefix, top 3 lexicographically.

---

### Solutions

#### Python
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.suggestions = []


class Solution:
    def suggestedProducts(self, products: list[str], searchWord: str) -> list[list[str]]:
        # start your solution
        products.sort()
        
        root = TrieNode()
        
        for product in products:
            node = root
            for char in product:
                if char not in node.children:
                    node.children[char] = TrieNode()
                node = node.children[char]
                if len(node.suggestions) < 3:
                    node.suggestions.append(product)
        
        result = []
        node = root
        
        for char in searchWord:
            if node and char in node.children:
                node = node.children[char]
                result.append(node.suggestions)
            else:
                node = None
                result.append([])
        
        return result
        # end your solution


def main():
    n = int(input())
    products = input().split()
    searchWord = input().strip()
    
    sol = Solution()
    result = sol.suggestedProducts(products, searchWord)
    
    for suggestions in result:
        if suggestions:
            print(" ".join(suggestions))
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
#include <algorithm>
#include <unordered_map>
#include <sstream>
using namespace std;

class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    vector<string> suggestions;
    
    TrieNode() {}
};

class Solution {
public:
    vector<vector<string>> suggestedProducts(vector<string>& products, string searchWord) {
        // start your solution
        sort(products.begin(), products.end());
        
        TrieNode* root = new TrieNode();
        
        for (const string& product : products) {
            TrieNode* node = root;
            for (char c : product) {
                if (node->children.find(c) == node->children.end()) {
                    node->children[c] = new TrieNode();
                }
                node = node->children[c];
                if (node->suggestions.size() < 3) {
                    node->suggestions.push_back(product);
                }
            }
        }
        
        vector<vector<string>> result;
        TrieNode* node = root;
        
        for (char c : searchWord) {
            if (node && node->children.find(c) != node->children.end()) {
                node = node->children[c];
                result.push_back(node->suggestions);
            } else {
                node = nullptr;
                result.push_back({});
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
    
    vector<string> products;
    stringstream ss(line);
    string product;
    while (ss >> product) {
        products.push_back(product);
    }
    
    string searchWord;
    getline(cin, searchWord);
    
    Solution sol;
    vector<vector<string>> result = sol.suggestedProducts(products, searchWord);
    
    for (const auto& suggestions : result) {
        if (suggestions.empty()) {
            cout << "none" << endl;
        } else {
            for (int i = 0; i < suggestions.size(); i++) {
                if (i > 0) cout << " ";
                cout << suggestions[i];
            }
            cout << endl;
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
    List<String> suggestions;
    
    TrieNode() {
        children = new HashMap<>();
        suggestions = new ArrayList<>();
    }
}

class Solution {
    public List<List<String>> suggestedProducts(String[] products, String searchWord) {
        // start your solution
        Arrays.sort(products);
        
        TrieNode root = new TrieNode();
        
        for (String product : products) {
            TrieNode node = root;
            for (char c : product.toCharArray()) {
                if (!node.children.containsKey(c)) {
                    node.children.put(c, new TrieNode());
                }
                node = node.children.get(c);
                if (node.suggestions.size() < 3) {
                    node.suggestions.add(product);
                }
            }
        }
        
        List<List<String>> result = new ArrayList<>();
        TrieNode node = root;
        
        for (char c : searchWord.toCharArray()) {
            if (node != null && node.children.containsKey(c)) {
                node = node.children.get(c);
                result.add(node.suggestions);
            } else {
                node = null;
                result.add(new ArrayList<>());
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
        String[] products = sc.nextLine().split(" ");
        String searchWord = sc.nextLine();
        
        Solution sol = new Solution();
        List<List<String>> result = sol.suggestedProducts(products, searchWord);
        
        for (List<String> suggestions : result) {
            if (suggestions.isEmpty()) {
                System.out.println("none");
            } else {
                System.out.println(String.join(" ", suggestions));
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
        self.suggestions = []


class Solution:
    def suggestedProducts(self, products: list[str], searchWord: str) -> list[list[str]]:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    products = input().split()
    searchWord = input().strip()
    
    sol = Solution()
    result = sol.suggestedProducts(products, searchWord)
    
    for suggestions in result:
        if suggestions:
            print(" ".join(suggestions))
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
#include <algorithm>
#include <unordered_map>
#include <sstream>
using namespace std;

class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    vector<string> suggestions;
    
    TrieNode() {}
};

class Solution {
public:
    vector<vector<string>> suggestedProducts(vector<string>& products, string searchWord) {
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
    
    vector<string> products;
    stringstream ss(line);
    string product;
    while (ss >> product) {
        products.push_back(product);
    }
    
    string searchWord;
    getline(cin, searchWord);
    
    Solution sol;
    vector<vector<string>> result = sol.suggestedProducts(products, searchWord);
    
    for (const auto& suggestions : result) {
        if (suggestions.empty()) {
            cout << "none" << endl;
        } else {
            for (int i = 0; i < suggestions.size(); i++) {
                if (i > 0) cout << " ";
                cout << suggestions[i];
            }
            cout << endl;
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
    List<String> suggestions;
    
    TrieNode() {
        children = new HashMap<>();
        suggestions = new ArrayList<>();
    }
}

class Solution {
    public List<List<String>> suggestedProducts(String[] products, String searchWord) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        sc.nextLine();
        String[] products = sc.nextLine().split(" ");
        String searchWord = sc.nextLine();
        
        Solution sol = new Solution();
        List<List<String>> result = sol.suggestedProducts(products, searchWord);
        
        for (List<String> suggestions : result) {
            if (suggestions.isEmpty()) {
                System.out.println("none");
            } else {
                System.out.println(String.join(" ", suggestions));
            }
        }
        
        sc.close();
    }
}
```
