# Kolkata Metro Seat Arrangement

### Problem Statement

The Kolkata Metro Rail Corporation is designing a new seating system for their trains. Each seat type is represented by a lowercase letter, and passengers have complained about sitting next to the same seat type repeatedly. The metro authorities want to rearrange seats so that no two adjacent seats are of the same type.

Given a string `s` representing the current seat arrangement, rearrange the seats such that no two adjacent seats are the same. If such an arrangement is possible, return any valid rearrangement. If not possible, return an empty string.

### Input Format

- A single line containing the string `s`

### Output Format

- Print the rearranged string, or "impossible" if no valid arrangement exists

### Constraints

- `1 <= s.length <= 500`
- `s` consists of lowercase English letters only

### Test Cases

#### Test Case 1
**Input:**
```
aab
```
**Output:**
```
aba
```
**Explanation:** "aba" has no adjacent same characters. "baa" would also be invalid.

---

#### Test Case 2
**Input:**
```
aaab
```
**Output:**
```
impossible
```
**Explanation:** 'a' appears 3 times in length 4. No matter how we arrange, two 'a's will be adjacent.

---

#### Test Case 3
**Input:**
```
aabb
```
**Output:**
```
abab
```
**Explanation:** "abab" or "baba" both work.

---

#### Test Case 4
**Input:**
```
abc
```
**Output:**
```
abc
```
**Explanation:** Already valid (or any permutation like "bac", "cab", etc.).

---

#### Test Case 5
**Input:**
```
aaabbbccc
```
**Output:**
```
abcabcabc
```
**Explanation:** Each character appears 3 times, can interleave perfectly.

---

#### Test Case 6
**Input:**
```
a
```
**Output:**
```
a
```
**Explanation:** Single character is always valid.

---

#### Test Case 7
**Input:**
```
aaaaabbbbbccccc
```
**Output:**
```
abcabcabcabcabc
```
**Explanation:** 5 of each, length 15. Can be arranged as alternating pattern.

---

### Solutions

#### Python
```python
import heapq
from collections import Counter


class Solution:
    def reorganizeString(self, s: str) -> str:
        # start your solution
        count = Counter(s)
        max_heap = [(-freq, char) for char, freq in count.items()]
        heapq.heapify(max_heap)
        
        # Check if possible: max frequency should not exceed (n+1)/2
        n = len(s)
        max_freq = -max_heap[0][0]
        if max_freq > (n + 1) // 2:
            return ""
        
        result = []
        prev_freq, prev_char = 0, ''
        
        while max_heap or prev_freq < 0:
            if prev_freq < 0 and not max_heap:
                return ""
            
            if max_heap:
                freq, char = heapq.heappop(max_heap)
                result.append(char)
                
                if prev_freq < 0:
                    heapq.heappush(max_heap, (prev_freq, prev_char))
                
                prev_freq = freq + 1  # Used one, so increment (remember it's negative)
                prev_char = char
            else:
                return ""
        
        return "".join(result)
        # end your solution


def main():
    s = input().strip()
    
    sol = Solution()
    result = sol.reorganizeString(s)
    
    if result:
        print(result)
    else:
        print("impossible")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <string>
#include <queue>
#include <unordered_map>
using namespace std;

class Solution {
public:
    string reorganizeString(string s) {
        // start your solution
        unordered_map<char, int> count;
        for (char c : s) {
            count[c]++;
        }
        
        priority_queue<pair<int, char>> maxHeap;
        for (auto& [ch, freq] : count) {
            maxHeap.push({freq, ch});
        }
        
        // Check if possible
        int n = s.length();
        if (maxHeap.top().first > (n + 1) / 2) {
            return "";
        }
        
        string result;
        pair<int, char> prev = {0, ' '};
        
        while (!maxHeap.empty() || prev.first > 0) {
            if (prev.first > 0 && maxHeap.empty()) {
                return "";
            }
            
            auto [freq, ch] = maxHeap.top();
            maxHeap.pop();
            result += ch;
            
            if (prev.first > 0) {
                maxHeap.push(prev);
            }
            
            prev = {freq - 1, ch};
        }
        
        return result;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string s;
    cin >> s;
    
    Solution sol;
    string result = sol.reorganizeString(s);
    
    if (result.empty()) {
        cout << "impossible" << endl;
    } else {
        cout << result << endl;
    }
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public String reorganizeString(String s) {
        // start your solution
        Map<Character, Integer> count = new HashMap<>();
        for (char c : s.toCharArray()) {
            count.put(c, count.getOrDefault(c, 0) + 1);
        }
        
        PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a, b) -> b[0] - a[0]);
        for (Map.Entry<Character, Integer> entry : count.entrySet()) {
            maxHeap.offer(new int[]{entry.getValue(), entry.getKey()});
        }
        
        // Check if possible
        int n = s.length();
        if (maxHeap.peek()[0] > (n + 1) / 2) {
            return "";
        }
        
        StringBuilder result = new StringBuilder();
        int[] prev = {0, ' '};
        
        while (!maxHeap.isEmpty() || prev[0] > 0) {
            if (prev[0] > 0 && maxHeap.isEmpty()) {
                return "";
            }
            
            int[] curr = maxHeap.poll();
            result.append((char) curr[1]);
            
            if (prev[0] > 0) {
                maxHeap.offer(prev);
            }
            
            prev = new int[]{curr[0] - 1, curr[1]};
        }
        
        return result.toString();
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.next();
        
        Solution sol = new Solution();
        String result = sol.reorganizeString(s);
        
        if (result.isEmpty()) {
            System.out.println("impossible");
        } else {
            System.out.println(result);
        }
        
        sc.close();
    }
}
```

### Code Stub

#### Python
```python
import heapq
from collections import Counter


class Solution:
    def reorganizeString(self, s: str) -> str:
        # start your solution
        
        
        
        # end your solution


def main():
    s = input().strip()
    
    sol = Solution()
    result = sol.reorganizeString(s)
    
    if result:
        print(result)
    else:
        print("impossible")


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <string>
#include <queue>
#include <unordered_map>
using namespace std;

class Solution {
public:
    string reorganizeString(string s) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    string s;
    cin >> s;
    
    Solution sol;
    string result = sol.reorganizeString(s);
    
    if (result.empty()) {
        cout << "impossible" << endl;
    } else {
        cout << result << endl;
    }
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public String reorganizeString(String s) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.next();
        
        Solution sol = new Solution();
        String result = sol.reorganizeString(s);
        
        if (result.isEmpty()) {
            System.out.println("impossible");
        } else {
            System.out.println(result);
        }
        
        sc.close();
    }
}
```