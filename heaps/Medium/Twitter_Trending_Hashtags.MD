# Twitter India Trending Hashtags

### Problem Statement

Twitter India's analytics team is building a trending hashtags feature for Indian users. They collect hashtags from recent tweets and need to find the k most frequently used hashtags.

Given an array of hashtag strings and an integer k, return the k most frequent hashtags. The answer should be sorted by frequency from highest to lowest. If two hashtags have the same frequency, they should be sorted in lexicographical (alphabetical) order.

### Input Format

- First line contains two integers: `n` (number of hashtags) and `k`
- Second line contains `n` space-separated strings representing hashtags

### Output Format

- Print k space-separated strings representing the k most frequent hashtags

### Constraints

- `1 <= n <= 500`
- `1 <= k <= number of unique hashtags`
- `1 <= words[i].length <= 10`
- `words[i]` consists of lowercase English letters only
- The answer is guaranteed to be unique

### Test Cases

#### Test Case 1
**Input:**
```
7 2
india love cricket india modi love india
```
**Output:**
```
india love
```
**Explanation:** "india" appears 3 times, "love" appears 2 times, "cricket" and "modi" appear 1 time each.

---

#### Test Case 2
**Input:**
```
4 4
diwali holi diwali holi
```
**Output:**
```
diwali holi
```
**Explanation:** Both appear twice. Sorted lexicographically: "diwali" before "holi".

---

#### Test Case 3
**Input:**
```
1 1
mumbai
```
**Output:**
```
mumbai
```
**Explanation:** Single hashtag.

---

#### Test Case 4
**Input:**
```
6 2
ipl ipl cricket cricket football hockey
```
**Output:**
```
cricket ipl
```
**Explanation:** "ipl" and "cricket" both appear 2 times. "cricket" < "ipl" lexicographically.

---

#### Test Case 5
**Input:**
```
5 3
a b c d e
```
**Output:**
```
a b c
```
**Explanation:** All have frequency 1, return first 3 in alphabetical order.

---

#### Test Case 6
**Input:**
```
10 3
chai chai chai coffee coffee tea milk milk milk milk
```
**Output:**
```
milk chai coffee
```
**Explanation:** milk(4) > chai(3) > coffee(2) > tea(1).

---

#### Test Case 7
**Input:**
```
8 2
zzz aaa zzz aaa bbb bbb ccc ccc
```
**Output:**
```
aaa bbb
```
**Explanation:** aaa, bbb, ccc, zzz all have frequency 2. Alphabetically: aaa < bbb < ccc < zzz. Top 2: aaa, bbb.

---

### Solutions

#### Python
```python
import heapq
from collections import Counter


class Solution:
    def topKFrequent(self, words: list[str], k: int) -> list[str]:
        # start your solution
        count = Counter(words)
        
        # Use min-heap with custom comparison
        # We want max frequency, but min lexicographic for ties
        # So we store (-freq, word) and use max heap behavior via negation
        heap = []
        
        for word, freq in count.items():
            heapq.heappush(heap, (-freq, word))
        
        result = []
        for _ in range(k):
            result.append(heapq.heappop(heap)[1])
        
        return result
        # end your solution


def main():
    first_line = input().split()
    n = int(first_line[0])
    k = int(first_line[1])
    
    words = input().split()
    
    sol = Solution()
    result = sol.topKFrequent(words, k)
    print(" ".join(result))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_map>
#include <string>
using namespace std;

class Solution {
public:
    vector<string> topKFrequent(vector<string>& words, int k) {
        // start your solution
        unordered_map<string, int> count;
        for (const string& word : words) {
            count[word]++;
        }
        
        // Custom comparator: higher freq first, then lexicographically smaller
        auto cmp = [](const pair<int, string>& a, const pair<int, string>& b) {
            if (a.first != b.first) return a.first < b.first;  // higher freq first
            return a.second > b.second;  // lexicographically smaller first
        };
        
        priority_queue<pair<int, string>, vector<pair<int, string>>, decltype(cmp)> maxHeap(cmp);
        
        for (auto& [word, freq] : count) {
            maxHeap.push({freq, word});
        }
        
        vector<string> result;
        for (int i = 0; i < k; i++) {
            result.push_back(maxHeap.top().second);
            maxHeap.pop();
        }
        
        return result;
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, k;
    cin >> n >> k;
    
    vector<string> words(n);
    for (int i = 0; i < n; i++) {
        cin >> words[i];
    }
    
    Solution sol;
    vector<string> result = sol.topKFrequent(words, k);
    
    for (int i = 0; i < result.size(); i++) {
        if (i > 0) cout << " ";
        cout << result[i];
    }
    cout << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        // start your solution
        Map<String, Integer> count = new HashMap<>();
        for (String word : words) {
            count.put(word, count.getOrDefault(word, 0) + 1);
        }
        
        // Max heap: higher frequency first, then lexicographically smaller
        PriorityQueue<Map.Entry<String, Integer>> maxHeap = new PriorityQueue<>((a, b) -> {
            if (!a.getValue().equals(b.getValue())) {
                return b.getValue() - a.getValue();  // higher freq first
            }
            return a.getKey().compareTo(b.getKey());  // lexicographically smaller first
        });
        
        maxHeap.addAll(count.entrySet());
        
        List<String> result = new ArrayList<>();
        for (int i = 0; i < k; i++) {
            result.add(maxHeap.poll().getKey());
        }
        
        return result;
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int k = sc.nextInt();
        
        String[] words = new String[n];
        for (int i = 0; i < n; i++) {
            words[i] = sc.next();
        }
        
        Solution sol = new Solution();
        List<String> result = sol.topKFrequent(words, k);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < result.size(); i++) {
            if (i > 0) sb.append(" ");
            sb.append(result.get(i));
        }
        System.out.println(sb.toString());
        
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
    def topKFrequent(self, words: list[str], k: int) -> list[str]:
        # start your solution
        
        
        
        # end your solution


def main():
    first_line = input().split()
    n = int(first_line[0])
    k = int(first_line[1])
    
    words = input().split()
    
    sol = Solution()
    result = sol.topKFrequent(words, k)
    print(" ".join(result))


if __name__ == "__main__":
    main()
```

#### C++
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_map>
#include <string>
using namespace std;

class Solution {
public:
    vector<string> topKFrequent(vector<string>& words, int k) {
        // start your solution
        
        
        
        // end your solution
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n, k;
    cin >> n >> k;
    
    vector<string> words(n);
    for (int i = 0; i < n; i++) {
        cin >> words[i];
    }
    
    Solution sol;
    vector<string> result = sol.topKFrequent(words, k);
    
    for (int i = 0; i < result.size(); i++) {
        if (i > 0) cout << " ";
        cout << result[i];
    }
    cout << endl;
    
    return 0;
}
```

#### Java
```java
import java.util.*;

class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        // start your solution
        
        
        
        // end your solution
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int k = sc.nextInt();
        
        String[] words = new String[n];
        for (int i = 0; i < n; i++) {
            words[i] = sc.next();
        }
        
        Solution sol = new Solution();
        List<String> result = sol.topKFrequent(words, k);
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < result.size(); i++) {
            if (i > 0) sb.append(" ");
            sb.append(result.get(i));
        }
        System.out.println(sb.toString());
        
        sc.close();
    }
}
```