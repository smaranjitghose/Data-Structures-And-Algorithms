# Mantra Pattern Finder

### Problem Statement

A Sanskrit scholar at Varanasi University is studying ancient texts. She has a long manuscript and wants to find all positions where a specific sacred mantra appears as an anagram (letters rearranged). This helps identify variations of the mantra used across different traditions.

Given a string `s` (the manuscript) and a string `p` (the mantra pattern), find all start indices of `p`'s anagrams in `s`. The output should be in ascending order of indices.

An anagram is a rearrangement of all letters of a word to form another word, using all original letters exactly once.

### Input Format

- First line contains the string `s` (manuscript)
- Second line contains the string `p` (mantra pattern)

### Output Format

- Print space-separated indices where anagrams of p start in s
- If no anagrams found, print `none`

### Constraints

- `1 <= s.length, p.length <= 3 * 10^4`
- `s` and `p` consist of lowercase English letters

### Test Cases

#### Test Case 1
**Input:**
```
cbaebabacd
abc
```
**Output:**
```
0 6
```
**Explanation:** "cba" at index 0 and "bac" at index 6 are anagrams of "abc".

---

#### Test Case 2
**Input:**
```
abab
ab
```
**Output:**
```
0 1 2
```
**Explanation:** "ab" at 0, "ba" at 1, "ab" at 2 are all anagrams of "ab".

---

#### Test Case 3
**Input:**
```
aaaaaaa
aa
```
**Output:**
```
0 1 2 3 4 5
```
**Explanation:** Every consecutive pair is an anagram of "aa".

---

#### Test Case 4
**Input:**
```
xyz
abc
```
**Output:**
```
none
```
**Explanation:** No anagram of "abc" exists in "xyz".

---

#### Test Case 5
**Input:**
```
acdcaeccde
c
```
**Output:**
```
1 3 6 8
```
**Explanation:** 'c' appears at indices 1, 3, 6, 8.

---

#### Test Case 6
**Input:**
```
baa
aa
```
**Output:**
```
1
```
**Explanation:** Only "aa" starting at index 1 is an anagram of "aa".

---

#### Test Case 7
**Input:**
```
abcdefg
dcba
```
**Output:**
```
none
```
**Explanation:** No window of length 4 is an anagram of "dcba" since 'd' appears at different positions.

---

### Solutions

#### Python
```python
class Solution:
    def findAnagrams(self, s: str, p: str) -> list[int]:
        # start your solution
        if len(p) > len(s):
            return []
        
        result = []
        p_count = {}
        s_count = {}
        
        for char in p:
            p_count[char] = p_count.get(char, 0) + 1
        
        for i in range(len(s)):
            char = s[i]
            s_count[char] = s_count.get(char, 0) + 1
            
            if i >= len(p):
                left_char = s[i - len(p)]
                s_count[left_char] -= 1
                if s_count[left_char] == 0:
                    del s_count[left_char]
            
            if s_count == p_count:
                result.append(i - len(p) + 1)
        
        return result
        # end your solution


def main():
    s = input().strip()
    p = input().strip()
    
    sol = Solution()
    result = sol.findAnagrams(s, p)
    
    if result:
        print(" ".join(map(str, result)))
    else:
        print("none")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <string>
#include <vector>
#include <unordered_map>
using namespace std;

class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        // start your solution
        vector<int> result;
        if (p.length() > s.length()) {
            return result;
        }
        
        unordered_map<char, int> pCount, sCount;
        
        for (char c : p) {
            pCount[c]++;
        }
        
        for (int i = 0; i < s.length(); i++) {
            sCount[s[i]]++;
            
            if (i >= p.length()) {
                char leftChar = s[i - p.length()];
                sCount[leftChar]--;
                if (sCount[leftChar] == 0) {
                    sCount.erase(leftChar);
                }
            }
            
            if (sCount == pCount) {
                result.push_back(i - p.length() + 1);
            }
        }
        
        return result;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string s, p;
    getline(cin, s);
    getline(cin, p);
    
    Solution sol;
    vector<int> result = sol.findAnagrams(s, p);
    
    if (result.empty()) {
        cout << "none" << endl;
    } else {
        for (int i = 0; i < result.size(); i++) {
            if (i > 0) cout << " ";
            cout << result[i];
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
    public List<Integer> findAnagrams(String s, String p) {
        // start your solution
        List<Integer> result = new ArrayList<>();
        if (p.length() > s.length()) {
            return result;
        }
        
        Map<Character, Integer> pCount = new HashMap<>();
        Map<Character, Integer> sCount = new HashMap<>();
        
        for (char c : p.toCharArray()) {
            pCount.put(c, pCount.getOrDefault(c, 0) + 1);
        }
        
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            sCount.put(c, sCount.getOrDefault(c, 0) + 1);
            
            if (i >= p.length()) {
                char leftChar = s.charAt(i - p.length());
                sCount.put(leftChar, sCount.get(leftChar) - 1);
                if (sCount.get(leftChar) == 0) {
                    sCount.remove(leftChar);
                }
            }
            
            if (sCount.equals(pCount)) {
                result.add(i - p.length() + 1);
            }
        }
        
        return result;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String s = sc.nextLine();
        String p = sc.nextLine();
        
        Solution sol = new Solution();
        List<Integer> result = sol.findAnagrams(s, p);
        
        if (result.isEmpty()) {
            System.out.println("none");
        } else {
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < result.size(); i++) {
                if (i > 0) sb.append(" ");
                sb.append(result.get(i));
            }
            System.out.println(sb.toString());
        }
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class Solution:
    def findAnagrams(self, s: str, p: str) -> list[int]:
        # start your solution
        
        
        
        # end your solution


def main():
    s = input().strip()
    p = input().strip()
    
    sol = Solution()
    result = sol.findAnagrams(s, p)
    
    if result:
        print(" ".join(map(str, result)))
    else:
        print("none")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <string>
#include <vector>
#include <unordered_map>
using namespace std;

class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string s, p;
    getline(cin, s);
    getline(cin, p);
    
    Solution sol;
    vector<int> result = sol.findAnagrams(s, p);
    
    if (result.empty()) {
        cout << "none" << endl;
    } else {
        for (int i = 0; i < result.size(); i++) {
            if (i > 0) cout << " ";
            cout << result[i];
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
    public List<Integer> findAnagrams(String s, String p) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String s = sc.nextLine();
        String p = sc.nextLine();
        
        Solution sol = new Solution();
        List<Integer> result = sol.findAnagrams(s, p);
        
        if (result.isEmpty()) {
            System.out.println("none");
        } else {
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < result.size(); i++) {
                if (i > 0) sb.append(" ");
                sb.append(result.get(i));
            }
            System.out.println(sb.toString());
        }
        
        sc.close();
    }
}
```