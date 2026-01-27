# Shortest News Headline Extract

### Problem Statement

A journalist at The Times of India needs to create a headline that contains all the key terms from a breaking story. Given the full article text and a set of required key characters, find the shortest continuous substring of the article that contains all the required characters (including duplicates if needed).

Given two strings `s` (the article) and `t` (required characters), return the minimum window substring of `s` such that every character in `t` (including duplicates) is included in the window. If no such substring exists, return an empty string.

The answer is guaranteed to be unique if it exists.

### Input Format

- First line contains the string `s` (article text)
- Second line contains the string `t` (required characters)

### Output Format

- The minimum window substring, or `none` if no valid window exists

### Constraints

- `1 <= s.length, t.length <= 10^5`
- `s` and `t` consist of uppercase and lowercase English letters

### Test Cases

#### Test Case 1
**Input:**
```
ADOBECODEBANC
ABC
```
**Output:**
```
BANC
```
**Explanation:** "BANC" is the shortest substring containing 'A', 'B', and 'C'.

---

#### Test Case 2
**Input:**
```
a
a
```
**Output:**
```
a
```
**Explanation:** The entire string is the minimum window.

---

#### Test Case 3
**Input:**
```
a
aa
```
**Output:**
```
none
```
**Explanation:** Need two 'a's but only one exists.

---

#### Test Case 4
**Input:**
```
ABCDEFGHIJKLMNOP
ACE
```
**Output:**
```
ABCDE
```
**Explanation:** "ABCDE" contains A, C, E and is the shortest such window.

---

#### Test Case 5
**Input:**
```
aaaaaaaaaaaabbbbbcdd
abcdd
```
**Output:**
```
abbbbbcdd
```
**Explanation:** Minimum window containing a, b, c, d, d.

---

#### Test Case 6
**Input:**
```
cabwefgewcwaefgcf
cae
```
**Output:**
```
cwae
```
**Explanation:** "cwae" is the shortest window containing c, a, e.

---

#### Test Case 7
**Input:**
```
ab
b
```
**Output:**
```
b
```
**Explanation:** Single character match.

---

### Solutions

#### Python
```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        # start your solution
        if len(t) > len(s):
            return ""
        
        t_count = {}
        for char in t:
            t_count[char] = t_count.get(char, 0) + 1
        
        required = len(t_count)
        formed = 0
        window_count = {}
        
        left = 0
        min_len = float('inf')
        min_start = 0
        
        for right in range(len(s)):
            char = s[right]
            window_count[char] = window_count.get(char, 0) + 1
            
            if char in t_count and window_count[char] == t_count[char]:
                formed += 1
            
            while formed == required:
                if right - left + 1 < min_len:
                    min_len = right - left + 1
                    min_start = left
                
                left_char = s[left]
                window_count[left_char] -= 1
                
                if left_char in t_count and window_count[left_char] < t_count[left_char]:
                    formed -= 1
                
                left += 1
        
        return "" if min_len == float('inf') else s[min_start:min_start + min_len]
        # end your solution


def main():
    s = input().strip()
    t = input().strip()
    
    sol = Solution()
    result = sol.minWindow(s, t)
    
    print(result if result else "none")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <string>
#include <unordered_map>
#include <climits>
using namespace std;

class Solution {
public:
    string minWindow(string s, string t) {
        // start your solution
        if (t.length() > s.length()) {
            return "";
        }
        
        unordered_map<char, int> tCount;
        for (char c : t) {
            tCount[c]++;
        }
        
        int required = tCount.size();
        int formed = 0;
        unordered_map<char, int> windowCount;
        
        int left = 0;
        int minLen = INT_MAX;
        int minStart = 0;
        
        for (int right = 0; right < s.length(); right++) {
            char c = s[right];
            windowCount[c]++;
            
            if (tCount.count(c) && windowCount[c] == tCount[c]) {
                formed++;
            }
            
            while (formed == required) {
                if (right - left + 1 < minLen) {
                    minLen = right - left + 1;
                    minStart = left;
                }
                
                char leftChar = s[left];
                windowCount[leftChar]--;
                
                if (tCount.count(leftChar) && windowCount[leftChar] < tCount[leftChar]) {
                    formed--;
                }
                
                left++;
            }
        }
        
        return minLen == INT_MAX ? "" : s.substr(minStart, minLen);
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string s, t;
    getline(cin, s);
    getline(cin, t);
    
    Solution sol;
    string result = sol.minWindow(s, t);
    
    cout << (result.empty() ? "none" : result) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public String minWindow(String s, String t) {
        // start your solution
        if (t.length() > s.length()) {
            return "";
        }
        
        Map<Character, Integer> tCount = new HashMap<>();
        for (char c : t.toCharArray()) {
            tCount.put(c, tCount.getOrDefault(c, 0) + 1);
        }
        
        int required = tCount.size();
        int formed = 0;
        Map<Character, Integer> windowCount = new HashMap<>();
        
        int left = 0;
        int minLen = Integer.MAX_VALUE;
        int minStart = 0;
        
        for (int right = 0; right < s.length(); right++) {
            char c = s.charAt(right);
            windowCount.put(c, windowCount.getOrDefault(c, 0) + 1);
            
            if (tCount.containsKey(c) && windowCount.get(c).intValue() == tCount.get(c).intValue()) {
                formed++;
            }
            
            while (formed == required) {
                if (right - left + 1 < minLen) {
                    minLen = right - left + 1;
                    minStart = left;
                }
                
                char leftChar = s.charAt(left);
                windowCount.put(leftChar, windowCount.get(leftChar) - 1);
                
                if (tCount.containsKey(leftChar) && windowCount.get(leftChar) < tCount.get(leftChar)) {
                    formed--;
                }
                
                left++;
            }
        }
        
        return minLen == Integer.MAX_VALUE ? "" : s.substring(minStart, minStart + minLen);
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String s = sc.nextLine();
        String t = sc.nextLine();
        
        Solution sol = new Solution();
        String result = sol.minWindow(s, t);
        
        System.out.println(result.isEmpty() ? "none" : result);
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        # start your solution
        
        
        
        # end your solution


def main():
    s = input().strip()
    t = input().strip()
    
    sol = Solution()
    result = sol.minWindow(s, t)
    
    print(result if result else "none")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <string>
#include <unordered_map>
#include <climits>
using namespace std;

class Solution {
public:
    string minWindow(string s, string t) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string s, t;
    getline(cin, s);
    getline(cin, t);
    
    Solution sol;
    string result = sol.minWindow(s, t);
    
    cout << (result.empty() ? "none" : result) << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public String minWindow(String s, String t) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        String s = sc.nextLine();
        String t = sc.nextLine();
        
        Solution sol = new Solution();
        String result = sol.minWindow(s, t);
        
        System.out.println(result.isEmpty() ? "none" : result);
        
        sc.close();
    }
}
```