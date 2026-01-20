# Ayurvedic Medicine Grouping

### Problem Statement

Dr. Sharma runs an Ayurvedic pharmacy in Rishikesh. He noticed that some medicine names are anagrams of each other (contain the same letters rearranged). He wants to group such medicines together for better inventory management.

Given an array of strings `medicines`, group the anagrams together. You may return the groups in any order.

### Input Format

- The first line contains an integer `n`, the number of medicines.
- The second line contains `n` space-separated strings.

### Output Format

- Print each group of anagrams on a separate line, with words space-separated.
- Groups can be printed in any order, words within a group can be in any order.

### Constraints

- `1 <= n <= 10^4`
- `0 <= medicines[i].length <= 100`
- `medicines[i]` consists of lowercase English letters

### Test Cases

#### Test Case 1
**Input:**
```
6
eat tea tan ate nat bat
```
**Output:**
```
eat tea ate
tan nat
bat
```
**Explanation:** "eat", "tea", "ate" are anagrams (same letters: a,e,t). "tan", "nat" are anagrams (a,n,t). "bat" has no anagram pair.

---

#### Test Case 2
**Input:**
```
1

```
**Output:**
```

```
**Explanation:** Single empty string. One group containing empty string.

---

#### Test Case 3
**Input:**
```
1
tulsi
```
**Output:**
```
tulsi
```
**Explanation:** Single medicine, forms its own group.

---

#### Test Case 4
**Input:**
```
4
neem meen abc cba
```
**Output:**
```
neem meen
abc cba
```
**Explanation:** "neem" and "meen" are anagrams. "abc" and "cba" are anagrams.

---

#### Test Case 5
**Input:**
```
3
amla amla amla
```
**Output:**
```
amla amla amla
```
**Explanation:** All three are identical (and thus anagrams). Single group.

---

#### Test Case 6
**Input:**
```
5
ginger regina ingerg root toor
```
**Output:**
```
ginger regina ingerg
root toor
```
**Explanation:** "ginger", "regina", "ingerg" share same letters. "root", "toor" are anagrams.

---

#### Test Case 7
**Input:**
```
4
abc def ghi jkl
```
**Output:**
```
abc
def
ghi
jkl
```
**Explanation:** No anagrams exist. Each medicine forms its own group.

---

### Solutions

#### Python

```python
class Solution:
    def groupMedicines(self, medicines: list[str]) -> list[list[str]]:
        # start your solution
        from collections import defaultdict
        
        groups = defaultdict(list)
        for med in medicines:
            key = ''.join(sorted(med))
            groups[key].append(med)
        
        return list(groups.values())
        # end your solution


def main():
    n = int(input())
    medicines = input().split() if n > 0 else ['']
    
    sol = Solution()
    result = sol.groupMedicines(medicines)
    
    for group in result:
        print(' '.join(group))


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

class Solution {
public:
    vector<vector<string>> groupMedicines(vector<string>& medicines) {
        // start your solution
        unordered_map<string, vector<string>> groups;
        
        for (string& med : medicines) {
            string key = med;
            sort(key.begin(), key.end());
            groups[key].push_back(med);
        }
        
        vector<vector<string>> result;
        for (auto& pair : groups) {
            result.push_back(pair.second);
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
    
    vector<string> medicines(n);
    string line;
    getline(cin, line);
    stringstream ss(line);
    for (int i = 0; i < n; i++) {
        ss >> medicines[i];
    }
    
    Solution sol;
    vector<vector<string>> result = sol.groupMedicines(medicines);
    
    for (auto& group : result) {
        for (int i = 0; i < group.size(); i++) {
            if (i > 0) cout << " ";
            cout << group[i];
        }
        cout << endl;
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public List<List<String>> groupMedicines(String[] medicines) {
        // start your solution
        Map<String, List<String>> groups = new HashMap<>();
        
        for (String med : medicines) {
            char[] chars = med.toCharArray();
            Arrays.sort(chars);
            String key = new String(chars);
            
            groups.computeIfAbsent(key, k -> new ArrayList<>()).add(med);
        }
        
        return new ArrayList<>(groups.values());
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = Integer.parseInt(sc.nextLine().trim());
        String[] medicines = n > 0 ? sc.nextLine().split(" ") : new String[]{""};
        
        Solution sol = new Solution();
        List<List<String>> result = sol.groupMedicines(medicines);
        
        for (List<String> group : result) {
            System.out.println(String.join(" ", group));
        }
        
        sc.close();
    }
}
```

---

### Code Stub

#### Python

```python
class Solution:
    def groupMedicines(self, medicines: list[str]) -> list[list[str]]:
        # start your solution
        
        
        
        # end your solution


def main():
    n = int(input())
    medicines = input().split() if n > 0 else ['']
    
    sol = Solution()
    result = sol.groupMedicines(medicines)
    
    for group in result:
        print(' '.join(group))


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

class Solution {
public:
    vector<vector<string>> groupMedicines(vector<string>& medicines) {
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
    
    vector<string> medicines(n);
    string line;
    getline(cin, line);
    stringstream ss(line);
    for (int i = 0; i < n; i++) {
        ss >> medicines[i];
    }
    
    Solution sol;
    vector<vector<string>> result = sol.groupMedicines(medicines);
    
    for (auto& group : result) {
        for (int i = 0; i < group.size(); i++) {
            if (i > 0) cout << " ";
            cout << group[i];
        }
        cout << endl;
    }
    
    return 0;
}
```

#### Java

```java
import java.util.*;

class Solution {
    public List<List<String>> groupMedicines(String[] medicines) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = Integer.parseInt(sc.nextLine().trim());
        String[] medicines = n > 0 ? sc.nextLine().split(" ") : new String[]{""};
        
        Solution sol = new Solution();
        List<List<String>> result = sol.groupMedicines(medicines);
        
        for (List<String> group : result) {
            System.out.println(String.join(" ", group));
        }
        
        sc.close();
    }
}
```
