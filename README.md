# 🚀 Placement Preparation Master Roadmap & TODO List (Sept 15 – Sept 30)

> **Tech Stack Focus**: **Python 3** (Coding/DSA) & **MySQL 8.0** (DBMS)  
> **Commitment**: ~7 Hours/Day (Self-Paced across the 4 Pillars)  
> **Structure**: **Pillar 1: Concept Deep-Dive** $\to$ **Pillar 2: Direct LeetCode Practice** $\to$ **Pillar 3: MySQL & Core CS** $\to$ **Pillar 4: Targeted Aptitude**  
> **Primary References**: [Striver's A2Z DSA Sheet](https://takeuforward.org/dsa/strivers-a2z-sheet-learn-dsa-a-to-z) & [LeetCode](https://leetcode.com/)

> [!IMPORTANT]
> **⚡ Core Placement Strategy & Subject Focus:**
> - **DSA (Heavy Focus):** Much of your focus must be on DSA and solving coding problems.
> - **DBMS / MySQL:** You only need to know *which command shall be used where and in which scenario* (e.g. joins vs subqueries, window functions vs group by, when to index).
> - **Operating Systems:** Study purely for *MCQs*; place priority on *numericals* (CPU scheduling waiting/turnaround times, Banker's algorithm safe sequence, page faults).
> - **Aptitude:** First *learn the concepts through worked examples*, then immediately practice examples.

---

## 🐍 Python DSA Standard Toolbox

```python
# 1. FAST I/O FOR ONLINE ASSESSMENTS
import sys
input = sys.stdin.readline

# 2. NEVER HIT RECURSION ERROR IN DEEP DFS / TREES
sys.setrecursionlimit(200000)

# 3. QUEUE / BFS: O(1) POP vs O(N) LIST POP
from collections import deque
q = deque([start_node])
curr = q.popleft()  # O(1) - NEVER use list.pop(0) which is O(N)!

# 4. FREQUENCY COUNTING
from collections import Counter, defaultdict
freq = Counter(arr)  # O(N) construction
adj = defaultdict(list)  # Avoids 'if node not in adj:' checks

# 5. HEAPS (PRIORITY QUEUE) - heapq is MIN-HEAP ONLY!
import heapq
min_heap = []
heapq.heappush(min_heap, val)
min_val = heapq.heappop(min_heap)
# For MAX-HEAP, invert the sign:
heapq.heappush(max_heap, -val)
max_val = -heapq.heappop(max_heap)

# 6. BINARY SEARCH (LOWER & UPPER BOUND)
import bisect
idx_lower = bisect.bisect_left(sorted_arr, target)   # First index where arr[i] >= target
idx_upper = bisect.bisect_right(sorted_arr, target)  # First index where arr[i] > target
```

---

# 📅 STAGE 1: Data Structures from the Ground Up (Sept 15 – Sept 20)

---

### 📌 Day 1 — Monday, Sept 15: Python Core Primitives (Lists, Strings, Math)

#### 🧠 Concept Deep-Dive & Mental Model
1. **Python Dynamic Arrays (Lists)**:
   - Python lists do not store contiguous values directly; they store an array of **pointers (references)** pointing to heap objects.
   - When a list fills up, Python over-allocates extra memory ($4, 8, 16, 25, \dots$), giving `.append()` amortized $O(1)$ time.
   - **Why `list.pop(0)` and `list.insert(0, val)` are $O(N)$**: Every subsequent pointer has to be moved one index to the left or right.
   - **Slicing**: `arr[start:end:step]` creates a completely new array, taking $O(K)$ time and space (where $K = \text{slice length}$).
2. **Strings & ASCII**:
   - Strings are immutable. In-place modification `s[0] = 'a'` throws a `TypeError`.
   - String concatenation in a loop (`s += char`) creates a new string every time ($O(N^2)$). Always append characters to a list and use `''.join(chars)` ($O(N)$).
   - ASCII conversions: `ord('a') = 97`, `ord('A') = 65`, `ord('0') = 48`, `chr(97) = 'a'`.
3. **Basic Math Invariants**:
   - Digit Extraction: `x % 10` gets the last digit; `x // 10` removes the last digit.
   - Counting digits: $\lfloor \log_{10}(N) \rfloor + 1$.
   - Sieve of Eratosthenes: To find primes up to $N$, start at 2 and mark multiples as non-prime. Inner loop starts from $i \times i$ (smaller multiples are already marked).

#### 💻 Direct Coding Practice
- [ ] 🟢 [Reverse String](https://leetcode.com/problems/reverse-string/) — *Two pointers swap from both ends in $O(1)$ space.*
- [ ] 🟢 [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) — *Skip non-alphanumeric characters with `.isalnum()`.*
- [ ] 🟡 [Reverse Integer](https://leetcode.com/problems/reverse-integer/) — *Handle 32-bit signed integer boundaries `[-2^31, 2^31 - 1]`.*
- [ ] 🟢 [Palindrome Number](https://leetcode.com/problems/palindrome-number/) — *Reverse only half of the integer without converting to string.*
- [ ] 🟡 [Rotate Array](https://leetcode.com/problems/rotate-array/) — *Reverse whole array, reverse first $k$, reverse rest.*
- [ ] 🟡 [Count Primes](https://leetcode.com/problems/count-primes/) — *Implement Sieve of Eratosthenes in $O(N \log \log N)$.*

#### 🐬 MySQL & Core CS
- **Concept**: RDBMS table structures, Primary Key (Unique + Not Null), Candidate Key, Foreign Key.
- **Syntax to write by hand**:
  ```sql
  CREATE TABLE Students (
      id INT PRIMARY KEY AUTO_INCREMENT,
      name VARCHAR(50) NOT NULL,
      email VARCHAR(100) UNIQUE,
      gpa DECIMAL(3, 2) CHECK (gpa >= 0.0 AND gpa <= 10.0)
  );
  ```
- [ ] 🟢 [Combine Two Tables](https://leetcode.com/problems/combine-two-tables/) — *Practice `LEFT JOIN` on LeetCode Database.*

#### 🎯 Aptitude: Ratio, Proportion & Partnerships
- **Concept**: Compounded ratio of $(a:b)$ and $(c:d)$ is $(ac : bd)$. Mean proportional of $a$ and $b$ is $\sqrt{ab}$.
- **Partnership Rule**: $\text{Profit}_A : \text{Profit}_B = (\text{Investment}_A \times \text{Time}_A) : (\text{Investment}_B \times \text{Time}_B)$.
- [ ] Solve 15 problems on [IndiaBIX Ratio and Proportion](https://www.indiabix.com/aptitude/ratio-and-proportion/).

---

### 📌 Day 2 — Tuesday, Sept 16: Dictionaries, Sets & Frequency Mapping

#### 🧠 Concept Deep-Dive & Mental Model
1. **Hash Tables Under the Hood**:
   - Keys are converted to a memory bucket index via `hash(key) % capacity`.
   - Average lookup, insert, and delete: $O(1)$.
   - Worst-case lookup: $O(N)$ when all keys hash to the same bucket (hash collision).
   - In Python, dict keys must be **hashable** (immutable types: integers, strings, tuples; NOT lists or dicts).
2. **`collections.Counter` and `collections.defaultdict`**:
   - `Counter(iterable)` automatically builds a frequency map in $O(N)$.
   - `c.most_common(k)` returns the $k$ most frequent items.
   - `defaultdict(list)` automatically creates an empty list for any unseen key, avoiding clumsy `if key not in d: d[key] = []`.
3. **Sets (Hash Sets)**:
   - Enforce uniqueness. Lookups `if x in my_set:` are $O(1)$ compared to $O(N)$ in lists.
   - Set operations: `s1 | s2` (Union), `s1 & s2` (Intersection), `s1 - s2` (Difference).

#### 💻 Direct Coding Practice
- [ ] 🟢 [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/) — *Check if `len(nums) != len(set(nums))` in $O(N)$.*
- [ ] 🟢 [Two Sum](https://leetcode.com/problems/two-sum/) — *Store seen elements in hash map: lookup `target - num` in $O(1)$.*
- [ ] 🟢 [Valid Anagram](https://leetcode.com/problems/valid-anagram/) — *Compare frequency maps using `Counter(s) == Counter(t)`.*
- [ ] 🟢 [First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/) — *Two-pass frequency lookup.*
- [ ] 🟢 [Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/) — *Use Python `set(nums1) & set(nums2)`.*
- [ ] 🟡 [Group Anagrams](https://leetcode.com/problems/group-anagrams/) — *Use sorted string or 26-element character count tuple as dict key.*
- [ ] 🟡 [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/) — *Put in set; only expand if `num - 1 not in set`.*

#### 🐬 MySQL & Core CS
- **Concept**: DML (`INSERT`, `UPDATE`, `DELETE`) vs `TRUNCATE` vs `DROP`.
- **Order of Clause Execution**: `FROM` $\to$ `WHERE` $\to$ `GROUP BY` $\to$ `HAVING` $\to$ `SELECT` $\to$ `ORDER BY` $\to$ `LIMIT`.
- [ ] 🟢 [Customers Who Never Order](https://leetcode.com/problems/customers-who-never-order/) — *Practice `LEFT JOIN ... WHERE ... IS NULL` or subquery with `NOT IN`.*

#### 🎯 Aptitude: Work & Time
- **The LCM / Total Units Method**:
  - Never add fractions like $\frac{1}{12} + \frac{1}{15}$.
  - Total Work = $\text{LCM}(12, 15) = 60$ units. Efficiency of A = $5$ units/day; B = $4$ units/day. Total rate = $9$ units/day. Time = $\frac{60}{9} = \frac{20}{3}$ days.
- **Men-Days Formula**: $\frac{M_1 \times D_1 \times H_1}{W_1} = \frac{M_2 \times D_2 \times H_2}{W_2}$.
- [ ] Solve 15–20 problems on [IndiaBIX Time and Work](https://www.indiabix.com/aptitude/time-and-work/).

---

### 📌 Day 3 — Wednesday, Sept 17: Recursion Mechanics & Sorting Algorithms

#### 🧠 Concept Deep-Dive & Mental Model
1. **Recursion Call Stack**:
   - Every function call pushes a new **stack frame** (local variables, parameters, return address) onto the OS call stack.
   - When base condition is met, frames pop off and return values up the tree.
   - If base condition is missing or recursion is too deep $\implies$ `RecursionError: maximum recursion depth exceeded`.
2. **Merge Sort (Divide & Conquer)**:
   - Divide: Split array into left and right halves at `mid = (low + high) // 2`.
   - Conquer: Recursively sort left and right halves.
   - Combine: Merge two sorted halves using two pointers.
   - Invariant: Guaranteed $O(N \log N)$ time in Best, Average, and Worst cases. Auxiliary space: $O(N)$.
3. **Quick Sort (Partitioning)**:
   - Pick a pivot (e.g. `arr[low]` or random element). Partition array such that elements $\le$ pivot are left, elements $>$ pivot are right.
   - Invariant: Average time $O(N \log N)$. Worst case $O(N^2)$ (when pivot is already the extreme in sorted array). Auxiliary space: $O(\log N)$ call stack.

#### 💻 Direct Coding Practice
- [ ] 🟢 [Fibonacci Number](https://leetcode.com/problems/fibonacci-number/) — *Write recursive, memoized, and iterative versions.*
- [ ] 🟡 [Pow(x, n)](https://leetcode.com/problems/powx-n/) — *Binary exponentiation: $x^n = (x^2)^{n/2}$ in $O(\log N)$.*
- [ ] 🟢 [Check if Array Is Sorted and Rotated](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/) — *Count dips `nums[i] > nums[(i+1)%n]`; must be $\le 1$.*
- [ ] 🟡 [Sort an Array (Merge Sort)](https://leetcode.com/problems/sort-an-array/) — *Implement Merge Sort from scratch without using `.sort()`.*

#### 🐬 MySQL & Core CS
- **Concept**: Aggregation functions (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`) + `GROUP BY` and `HAVING`.
- **Difference between WHERE and HAVING**: `WHERE` filters rows *before* grouping; `HAVING` filters aggregated summaries *after* grouping.
- [ ] 🟢 [Duplicate Emails](https://leetcode.com/problems/duplicate-emails/) — *Practice `GROUP BY email HAVING COUNT(email) > 1` on LeetCode.*

#### 🎯 Aptitude: Pipes & Cisterns
- **Concept**: Inflow pipe = positive efficiency ($+$); Leak / Outflow pipe = negative efficiency ($-$).
- Watch out for alternate-hour problems: calculate net progress per cycle of 2 hours, and calculate the final hour carefully when the inlet fills the tank before the leak can drain it.
- [ ] Solve 15 problems on [IndiaBIX Pipes and Cistern](https://www.indiabix.com/aptitude/pipes-and-cistern/).

---

### 📌 Day 4 — Thursday, Sept 18: Linked Lists from Scratch

#### 🧠 Concept Deep-Dive & Mental Model
1. **Node Structure**:
   ```python
   class ListNode:
       def __init__(self, val=0, next=None):
           self.val = val
           self.next = next
   ```
2. **The Dummy Node Pattern**:
   - When deleting or reordering nodes, the `head` pointer might change.
   - Creating `dummy = ListNode(0); dummy.next = head` ensures you have a permanent anchor before `head`. Always return `dummy.next`.
3. **Fast & Slow Pointers (Floyd’s Cycle Algorithm)**:
   - `slow` advances 1 step, `fast` advances 2 steps.
   - **Middle of List**: When `fast` reaches the end (`fast is None or fast.next is None`), `slow` is guaranteed to be at the middle.
   - **Cycle Detection**: If there is a cycle of length $C$, the relative speed between `fast` and `slow` is $2 - 1 = 1$. `fast` closes the gap by 1 node each step and must collide with `slow`.

#### 💻 Direct Coding Practice
- [ ] 🟡 [Design Linked List](https://leetcode.com/problems/design-linked-list/) — *Implement `get`, `addAtHead`, `addAtTail`, `addAtIndex`, `deleteAtIndex`.*
- [ ] 🟢 [Delete Node in a Linked List](https://leetcode.com/problems/delete-node-in-a-linked-list/) — *Trick: Copy value of next node into current node, then bypass next node.*
- [ ] 🟢 [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) — *Classic 3-pointer iterative rewiring: `prev`, `curr`, `next_temp`.*
- [ ] 🟢 [Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/) — *Fast and slow pointer approach.*
- [ ] 🟢 [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) — *Detect cycle using Floyd’s algorithm.*
- [ ] 🟡 [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/) — *Find starting node of the cycle.*
- [ ] 🟢 [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/) — *Splice lists using dummy node in $O(N + M)$.*

#### 🐬 MySQL & Core CS
- **Concept**: SQL Joins (`INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`).
- **MySQL Full Outer Join**: MySQL doesn't have `FULL OUTER JOIN`; write:
  ```sql
  SELECT * FROM TableA LEFT JOIN TableB ON TableA.id = TableB.id
  UNION
  SELECT * FROM TableA RIGHT JOIN TableB ON TableA.id = TableB.id;
  ```
- [ ] 🟢 [Employees Earning More Than Their Managers](https://leetcode.com/problems/employees-earning-more-than-their-managers/) — *Practice Self-Join on LeetCode Database.*

#### 🎯 Aptitude: Speed, Distance & Time
- **Formulas**:
  - $1\text{ km/h} = \frac{5}{18}\text{ m/s}$; $1\text{ m/s} = \frac{18}{5}\text{ km/h}$.
  - Average Speed for equal distances: $\frac{2xy}{x+y}$.
  - Relative Speed: Opposite direction $\implies S_1 + S_2$; Same direction $\implies |S_1 - S_2|$.
  - Train crossing a pole: Distance = $L_{\text{train}}$. Crossing platform: Distance = $L_{\text{train}} + L_{\text{platform}}$.
  - Boats: Downstream = $B + C$, Upstream = $B - C$.
- [ ] Solve 15–20 problems on [IndiaBIX Speed and Distance](https://www.indiabix.com/aptitude/time-and-distance/).

---

### 📌 Day 5 — Friday, Sept 19: Stacks & Queues from Scratch

#### 🧠 Concept Deep-Dive & Mental Model
1. **Stack (LIFO - Last In First Out)**:
   - Python implementation: `list` with `.append(x)` (push) and `.pop()` (pop). Both are $O(1)$.
   - Top of stack: `stack[-1]`.
2. **Queue (FIFO - First In First Out)**:
   - Python implementation: `from collections import deque`.
   - Enqueue: `q.append(x)` ($O(1)$); Dequeue: `q.popleft()` ($O(1)$).
3. **Monotonic Stack Pattern**:
   - A stack that maintains its elements in monotonically increasing or decreasing order.
   - For **Next Greater Element**: Iterate from right to left. While `stack and stack[-1] <= nums[i]`, pop. If stack is not empty, `nge[i] = stack[-1]`. Push `nums[i]`.
   - Every element is pushed and popped at most once $\implies$ Total time $O(N)$!

#### 💻 Direct Coding Practice
- [ ] 🟢 [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) — *Stack matching opening and closing brackets.*
- [ ] 🟢 [Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/) — *Rotate queue by `len(q) - 1` on push.*
- [ ] 🟢 [Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/) — *Two stacks: `in_stack` and `out_stack`.*
- [ ] 🟡 [Min Stack](https://leetcode.com/problems/min-stack/) — *Store `(val, current_min)` pairs in $O(1)$.*
- [ ] 🟢 [Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/) — *Monotonic stack + hash map.*

#### 🐬 MySQL & Core CS
- **Concept**: Subqueries (Single-row, Multi-row with `IN`, `EXISTS`).
- **Classic Interview Query: Second Highest Salary**:
  ```sql
  -- Handled gracefully returning NULL if no 2nd highest salary exists:
  SELECT (
      SELECT DISTINCT salary 
      FROM Employee 
      ORDER BY salary DESC 
      LIMIT 1 OFFSET 1
  ) AS SecondHighestSalary;
  ```
- [ ] 🟡 [Second Highest Salary](https://leetcode.com/problems/second-highest-salary/) — *Solve directly on LeetCode Database.*

#### 🎯 Aptitude: Syllogisms
- **Rules of Deductive Logic**:
  - Statements are 100% true, even if they contradict real-world facts ("All cats are dogs").
  - **Venn Diagram Representation**:
    - "All A are B" $\implies$ Circle A inside Circle B.
    - "Some A are B" $\implies$ Overlapping intersection.
    - "No A is B" $\implies$ Two disconnected circles with a line and cross.
    - "Some A are not B" $\implies$ Shaded region of A strictly outside B.
  - **"Either-Or" Test**: (1) Both conclusions individually false, (2) Same subject and predicate, (3) Complementary pair (*Some + No* OR *All + Some Not*).
  - **"Possibility" Test**: If any single valid Venn diagram makes the conclusion true, the possibility is TRUE.
- [ ] Solve 20 questions on [IndiaBIX Syllogism](https://www.indiabix.com/logical-reasoning/syllogism/).

---

### 📌 Day 6 — Saturday, Sept 20: Trees & Binary Search Fundamentals

#### 🧠 Concept Deep-Dive & Mental Model
1. **Tree Representation in Python**:
   ```python
   class TreeNode:
       def __init__(self, val=0, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right
   ```
2. **The 4 Tree Traversals**:
   - **Preorder (Root $\to$ Left $\to$ Right)**: Process root first.
   - **Inorder (Left $\to$ Root $\to$ Right)**: In a Binary Search Tree (BST), this visits nodes in strictly sorted order!
   - **Postorder (Left $\to$ Right $\to$ Root)**: Computes properties of subtrees before processing current node (e.g. tree height, tree deletion).
   - **Level-Order (BFS)**: Uses a `collections.deque` to traverse level-by-level.
3. **Binary Search Framework**:
   - Works strictly on sorted data.
   - `low = 0`, `high = len(arr) - 1`. While `low <= high`: `mid = (low + high) // 2`.
   - If `arr[mid] == target`, return `mid`.
   - If `arr[mid] < target`, `low = mid + 1`. Else `high = mid - 1`.
   - Time: $O(\log N)$, Space: $O(1)$.

#### 💻 Direct Coding Practice
- [ ] 🟢 [Binary Search](https://leetcode.com/problems/binary-search/) — *Standard iterative binary search.*
- [ ] 🟢 [Search Insert Position](https://leetcode.com/problems/search-insert-position/) — *Find insertion point (`bisect_left` lower bound logic).*
- [ ] 🟢 [Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/) — *Recursive and iterative.*
- [ ] 🟢 [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/) — *Recursive and iterative with stack.*
- [ ] 🟢 [Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/) — *Bottom-up traversal.*
- [ ] 🟢 [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/) — *`1 + max(depth(left), depth(right))`.*
- [ ] 🟡 [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) — *BFS using `deque` with level size.*

#### 🐬 MySQL & Core CS (Operating Systems)
- **Concept**:
  - **Process vs Thread**: Process has its own virtual address space; Threads share address space, heap, and open files of parent process, but have individual stack frames and registers.
  - **CPU Scheduling**: First Come First Served (FCFS), Shortest Job First (SJF - optimal average wait time), Round Robin (RR - uses time slice / quantum).
  - **Python Interview Question**: What is Python's GIL (Global Interpreter Lock)? A mutex that prevents multiple native threads from executing Python bytecodes at once, making CPU-bound multi-threading non-parallel in standard CPython.

#### 🎯 Aptitude: Numeric Patterns & Series
- **Types of Number Series**:
  - Prime number series: $2, 3, 5, 7, 11, 13, 17, 19, \dots$
  - Difference of differences: Take $\Delta_1$, then $\Delta_2$ (often constant or forming an AP).
  - Alternating series: Two independent sequences merged into odd and even indices.
  - Squares and Cubes: $n^2 \pm 1$, $n^3 \pm 1$, $n^3 + n^2$.
- [ ] Solve 25 questions on [IndiaBIX Number Series](https://www.indiabix.com/logical-reasoning/number-series/).

---

# 📅 STAGE 2: Pattern-Based Problem Solving (Sept 21 – Sept 27)

---

### 📌 Day 7 — Sunday, Sept 21: Arrays — Two Pointers & Prefix Sum

#### 🧠 Concept Deep-Dive & Mental Model
1. **Kadane’s Algorithm (Maximum Subarray Sum)**:
   - At each element `x`, decide: Do I join the previous running subarray (`curr_sum + x`), or do I start a new subarray from `x`?
   - `curr_sum = max(x, curr_sum + x); max_sum = max(max_sum, curr_sum)`. Time: $O(N)$, Space: $O(1)$.
2. **Dutch National Flag (DNF) Algorithm**:
   - 3 pointers: `low`, `mid`, `high`.
   - Invariant: `arr[0 ... low-1] == 0`, `arr[low ... mid-1] == 1`, `arr[high+1 ... n-1] == 2`.
   - If `arr[mid] == 0`: swap with `arr[low]`, `low += 1, mid += 1`.
   - If `arr[mid] == 1`: `mid += 1`.
   - If `arr[mid] == 2`: swap with `arr[high]`, `high -= 1`. Single pass $O(N)$!
3. **Prefix Sum + Hash Map**:
   - Let `prefix[j]` be sum from $0 \dots j$. If `prefix[j] - prefix[i] = k`, then subarray from $i+1 \dots j$ has sum $k$.
   - Store count of each prefix sum in a dictionary. Initialize `d = {0: 1}` to handle subarrays starting from index 0.

#### 💻 Direct Coding Practice
- [ ] 🟡 [Maximum Subarray (Kadane's)](https://leetcode.com/problems/maximum-subarray/) — *Max subarray sum in $O(N)$.*
- [ ] 🟡 [Sort Colors (Dutch National Flag)](https://leetcode.com/problems/sort-colors/) — *Sort 0s, 1s, 2s in-place in 1 pass.*
- [ ] 🟢 [Majority Element](https://leetcode.com/problems/majority-element/) — *Moore’s Voting Algorithm in $O(N)$ time, $O(1)$ space.*
- [ ] 🟡 [3Sum](https://leetcode.com/problems/3sum/) — *Sort + Two Pointers. Skip duplicate values.*
- [ ] 🟡 [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) — *Prefix Sum + Hash Map in $O(N)$.*

#### 🐬 MySQL & Core CS
- **Concept**: Database Normalization (1NF, 2NF, 3NF, BCNF).
  - 1NF: Atomic values (no multiple values in one column).
  - 2NF: 1NF + No Partial Dependency (all non-key columns depend on full primary key).
  - 3NF: 2NF + No Transitive Dependency ($A \to B$ and $B \to C$).
  - BCNF: For every functional dependency $X \to Y$, $X$ must be a super key.
- [ ] 🟢 [Delete Duplicate Emails](https://leetcode.com/problems/delete-duplicate-emails/) — *Practice Self-Join deletion on LeetCode Database.*

#### 🎯 Aptitude: Alphabet & Alpha-Numeric Patterns
- **Techniques**:
  - Memorize **EJOTY**: $E=5, J=10, O=15, T=20, Y=25$.
  - Reverse letter pairs (sum of positions = 27): $A(1) \leftrightarrow Z(26)$, $B(2) \leftrightarrow Y(25)$, $C(3) \leftrightarrow X(24)$, $D(4) \leftrightarrow W(23)$, $E(5) \leftrightarrow V(22)$, $M(13) \leftrightarrow N(14)$.
- [ ] Solve 20 questions on [IndiaBIX Letter and Symbol Series](https://www.indiabix.com/logical-reasoning/letter-and-symbol-series/).

---

### 📌 Day 8 — Monday, Sept 22: Binary Search — Arrays & Search Space

#### 🧠 Concept Deep-Dive & Mental Model
1. **Binary Search on Rotated Sorted Array**:
   - In any rotated sorted array, when split at `mid`, **at least one half is ALWAYS completely sorted**.
   - If `nums[low] <= nums[mid]`: the left half is sorted. Check if target lies between `nums[low]` and `nums[mid]`.
   - Else: the right half is sorted. Check if target lies between `nums[mid]` and `nums[high]`.
2. **Binary Search on Answer (Search Space)**:
   - Used when we need to find the **minimum valid** or **maximum valid** value of a metric.
   - The answer lies in a bounded monotonic range: $[low, high]$.
   - Write a helper predicate function `def is_valid(candidate): ...`.
   - If `is_valid(mid)` is true, record answer and try to find a better one (e.g. `high = mid - 1`); else `low = mid + 1`.

#### 💻 Direct Coding Practice
- [ ] 🟡 [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) — *Check which half is sorted.*
- [ ] 🟡 [Find First and Last Position of Element](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) — *Run binary search twice for first and last bound.*
- [ ] 🟡 [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) — *Locate the inflection point.*
- [ ] 🟡 [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) — *Binary search on eating speed from $1 \dots \max(\text{piles})$.*
- [ ] 🟡 [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) — *Search space: $[\max(\text{weights}), \text{sum}(\text{weights})]$.*

#### 🐬 MySQL & Core CS (Operating Systems)
- **Concept**: Deadlocks.
  - 4 Coffman Conditions: (1) Mutual Exclusion, (2) Hold and Wait, (3) No Preemption, (4) Circular Wait.
  - Banker’s Algorithm for Deadlock Avoidance: Allocates resources only if system remains in a "Safe State".
  - Mutex vs Semaphore: Mutex has ownership (locking); Semaphore is a signaling counter.

#### 🎯 Aptitude: Case Study Puzzles 1 (Linear Seating + Multi-Attributes)
- **Framework**:
  - Scenario: 6 people (A, B, C, D, E, F) sit in a row facing North. Each lives in a different city (Delhi, Mumbai, Chennai, Pune, Kolkata, Bengaluru).
  - **The 2-Case Method**: Draw two parallel setups:
    - Case 1: Extreme left anchor.
    - Case 2: Extreme right anchor.
  - Fill definite clues first. Place relative clues next. Cross out the case that creates a contradiction.
- [ ] Practice 3 complete linear seating case study sets on [IndiaBIX Seating Arrangement](https://www.indiabix.com/logical-reasoning/seating-arrangement/).

---

### 📌 Day 9 — Tuesday, Sept 23: Sliding Window & Two Pointers

#### 🧠 Concept Deep-Dive & Mental Model
1. **Dynamic Sliding Window Mechanics**:
   - `left = 0`, iterate `right` from $0 \dots n-1$.
   - **Step 1 (Expand)**: Add `s[right]` to window state (frequency map / set / sum).
   - **Step 2 (Shrink)**: While window condition is violated, remove `s[left]` and advance `left += 1`.
   - **Step 3 (Update Answer)**: Window is now valid $\implies$ update `max_len = max(max_len, right - left + 1)`.
   - Time: $O(N)$ because both `left` and `right` only advance forward.

#### 💻 Direct Coding Practice
- [ ] 🟡 [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) — *Store last seen index of each char.*
- [ ] 🟡 [Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/) — *Window with at most $k$ zeros.*
- [ ] 🟡 [Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/) — *Window with at most 2 distinct elements.*
- [ ] 🟡 [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/) — *Window size minus max frequency $\le k$.*
- [ ] 🔴 [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/) — *Dynamic frequency matching window.*

#### 🐬 MySQL & Core CS
- **Concept**: MySQL 8.0 Window Functions (`ROW_NUMBER`, `RANK`, `DENSE_RANK`).
  - `ROW_NUMBER()`: 1, 2, 3 (no ties).
  - `RANK()`: 1, 1, 3 (ties skip ranks).
  - `DENSE_RANK()`: 1, 1, 2 (ties do not skip ranks).
- [ ] 🟡 [Nth Highest Salary](https://leetcode.com/problems/nth-highest-salary/) — *Solve using `DENSE_RANK()` or `LIMIT 1 OFFSET N-1` on LeetCode.*
- [ ] 🟡 [Department Highest Salary](https://leetcode.com/problems/department-highest-salary/) — *Practice `PARTITION BY` on LeetCode Database.*

#### 🎯 Aptitude: Case Study Puzzles 2 (Circular Seating + Multi-Attributes)
- **Framework**:
  - Facing **Center**: Clockwise = to the **Left**; Anti-Clockwise = to the **Right**.
  - Facing **Outside**: Clockwise = to the **Right**; Anti-Clockwise = to the **Left**.
  - Opposite Rule: In an 8-person circle, opposite people have exactly 3 people between them.
- [ ] Practice 3 complete circular seating case study sets on [IndiaBIX Seating Arrangement](https://www.indiabix.com/logical-reasoning/seating-arrangement/).

---

### 📌 Day 10 — Wednesday, Sept 24: Linked Lists & Monotonic Stacks

#### 🧠 Concept Deep-Dive & Mental Model
1. **Advanced Linked List Manipulation**:
   - Fast & Slow pointers separated by $K$ nodes: Advance `fast` $K$ steps forward first. Then move both together until `fast.next is None`. `slow.next` is the node to delete!
2. **Monotonic Stack Width Invariants**:
   - In histogram problems, a bar can expand left and right as long as adjacent bars are $\ge$ its height.
   - Using a monotonic increasing stack of indices, when a smaller bar arrives, the popped bar's width is bounded by current index (right) and the new stack top (left). Time: $O(N)$.

#### 💻 Direct Coding Practice
- [ ] 🟡 [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) — *Two pointers separated by $N$ steps.*
- [ ] 🔴 [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/) — *Use `heapq` with `(node.val, i, node)` tuples in $O(N \log K)$.*
- [ ] 🟡 [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/) — *Monotonic decreasing stack of indices.*
- [ ] 🔴 [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/) — *Monotonic stack width computation in $O(N)$.*

#### 🐬 MySQL & Core CS
- **Concept**:
  - **B+ Tree Indexing**: Clustered Index (data rows stored in Primary Key leaves) vs Secondary Index (leaves store pointer to Primary Key).
  - **ACID Properties**: Atomicity, Consistency, Isolation, Durability.
  - **4 Isolation Levels**: Read Uncommitted (dirty reads), Read Committed, Repeatable Read (MySQL default, prevents phantom reads via next-key locks), Serializable.
- [ ] 🟡 [Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries/) — *Practice `DENSE_RANK() <= 3` on LeetCode Database.*

#### 🎯 Aptitude: Permutations & Combinations (Part 1)
- **Formulas & Word Arrangements**:
  - Fundamental counting principle: Multiplication rule ($A \text{ and } B$) vs Addition rule ($A \text{ or } B$).
  - Word Anagrams with Repeated Letters: $\frac{N!}{p! \cdot q! \cdot r!}$.
  - **Vowels Together (Stringing Method)**: Treat all vowels as a single block $[V_1 V_2 V_3]$. Arrange the blocks, then arrange vowels internally.
  - **Vowels Separated (Gap Method)**: Place consonants first $\_ C_1 \_ C_2 \_ C_3 \_$. Choose from the available gaps for the vowels.
- [ ] Solve 20 questions on [IndiaBIX Permutation and Combination](https://www.indiabix.com/aptitude/permutation-and-combination/).

---

### 📌 Day 11 — Thursday, Sept 25: Binary Trees & Binary Search Trees

#### 🧠 Concept Deep-Dive & Mental Model
1. **Lowest Common Ancestor (LCA)**:
   - In Binary Tree: Traverse bottom-up. If current node equals $p$ or $q$, return node. If both left and right recursive calls return non-null, current node is the LCA!
   - In Binary Search Tree (BST): If both $p$ and $q$ are smaller than root, LCA is in left subtree. If both are greater, LCA is in right subtree. If they split on either side, root is the LCA!
2. **BST Invariant**:
   - Inorder traversal of a valid BST is strictly ascending.
   - For recursive validation, pass valid range: `validate(node.left, low, node.val)` and `validate(node.right, node.val, high)`.

#### 💻 Direct Coding Practice
- [ ] 🟢 [Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/) — *`max(diameter, left_height + right_height)`.*
- [ ] 🟡 [Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) — *Recursive subtree match.*
- [ ] 🟢 [Lowest Common Ancestor of a BST](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/) — *Directional split in $O(\log N)$.*
- [ ] 🟡 [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) — *Check range `(low, high)`.*
- [ ] 🟡 [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/) — *BFS level last element.*

#### 🐬 MySQL & Core CS (Computer Networks)
- **Concept**:
  - 7 Layers of OSI: Physical, Data Link, Network (IP), Transport (TCP/UDP), Session, Presentation, Application (HTTP/DNS).
  - **TCP 3-Way Handshake**: Client sends `SYN`, Server replies `SYN-ACK`, Client confirms with `ACK`.
  - **DNS Resolution**: Local cache $\to$ Recursive resolver $\to$ Root server $\to$ TLD server (.com) $\to$ Authoritative nameserver.
  - HTTP vs HTTPS: HTTPS runs over SSL/TLS port 443 (asymmetric encryption during handshake for key exchange, symmetric encryption for fast payload transfer).

#### 🎯 Aptitude: Permutations & Combinations (Part 2)
- **Combinations & Geometry**:
  - Selections: $^nC_r = \frac{n!}{r!(n - r)!}$.
  - Handshake / Matches formula: $^nC_2 = \frac{n(n-1)}{2}$.
  - Diagonals of an $n$-sided polygon: $^nC_2 - n = \frac{n(n-3)}{2}$.
  - Triangles from $n$ points with $m$ collinear: $^nC_3 - ^mC_3$.
  - Circular Permutation: $(n-1)!$; for garlands/necklaces: $\frac{(n-1)!}{2}$.
- [ ] Solve 20 questions on [IndiaBIX Permutation and Combination](https://www.indiabix.com/aptitude/permutation-and-combination/).

---

### 📌 Day 12 — Friday, Sept 26: Graphs — Representation, BFS & DFS

#### 🧠 Concept Deep-Dive & Mental Model
1. **Graph Representation**:
   ```python
   adj = collections.defaultdict(list)
   for u, v in edges:
       adj[u].append(v)
       adj[v].append(u)  # If undirected
   ```
2. **BFS vs DFS**:
   - **BFS (Queue)**: Explores concentric circles of distance $1, 2, 3, \dots$ Guaranteed to find **shortest path** in unweighted graphs.
   - **DFS (Recursion / Stack)**: Dives deeply down one path until hitting a dead end, then backtracks.
3. **Cycle Detection in Directed Graphs**:
   - Need two tracking sets: `visited` (global) and `path_visited` / recursion stack (current branch).
   - If we visit a neighbor that is already in `path_visited`, a back-edge and cycle exists!
   - Alternatively: Kahn's Algorithm (Topological Sort with In-Degree array).

#### 💻 Direct Coding Practice
- [ ] 🟡 [Number of Provinces](https://leetcode.com/problems/number-of-provinces/) — *Count connected components using BFS/DFS.*
- [ ] 🟡 [Number of Islands](https://leetcode.com/problems/number-of-islands/) — *Grid DFS: Sink visited land cells from `'1'` to `'0'`.*
- [ ] 🟡 [Rotting Oranges](https://leetcode.com/problems/rotting-oranges/) — *Multi-source BFS using `deque`.*
- [ ] 🟡 [Course Schedule](https://leetcode.com/problems/course-schedule/) — *Cycle detection in directed graph using Kahn's algorithm.*
- [ ] 🟡 [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/) — *Return topological sort order.*

#### 🐬 MySQL & Core CS (Operating Systems)
- **Concept**: Virtual Memory & Paging.
  - Page Table: Maps logical pages to physical frames.
  - Page Fault: Happens when CPU references a page not present in physical RAM; triggers OS trap to fetch page from disk.
  - Page Replacement: FIFO (suffers from Belady's Anomaly), LRU (Least Recently Used), Optimal (theoretical benchmark).
- [ ] 🟡 [Consecutive Numbers](https://leetcode.com/problems/consecutive-numbers/) — *Practice `LEAD()` / `LAG()` or 3-way join on LeetCode Database.*

#### 🎯 Aptitude: Probability
- **Core Formulas**:
  - $P(E) = \frac{\text{Favorable Outcomes}}{\text{Total Outcomes}}$.
  - **"At Least 1" Rule**:
    $$P(\text{At least 1 success}) = 1 - P(\text{Zero successes})$$
  - Cards Distribution: 52 total cards (13 Spades ♠, 13 Clubs ♣, 13 Hearts ♥, 13 Diamonds ♦). 12 Face cards (4 Jack, 4 Queen, 4 King). 4 Aces.
- [ ] Solve 20 questions on [IndiaBIX Probability](https://www.indiabix.com/aptitude/probability/).

---

### 📌 Day 13 — Saturday, Sept 27: Dynamic Programming — 1D & Grid Patterns

#### 🧠 Concept Deep-Dive & Mental Model
1. **When does DP apply?**
   - **Overlapping Subproblems**: Same sub-states are computed repeatedly.
   - **Optimal Substructure**: Optimal solution to problem incorporates optimal solutions to sub-problems.
2. **The 4 Transformation Steps**:
   1. Recursive function: `f(index, state)`.
   2. Memoization: Store results in `@cache` or dictionary to eliminate exponential time.
   3. Tabulation: Build iterative bottom-up table `dp = [0] * (n + 1)`.
   4. Space Optimization: If `dp[i]` only depends on `dp[i-1]` and `dp[i-2]`, replace the table with 2 scalar variables!

#### 💻 Direct Coding Practice
- [ ] 🟢 [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/) — *`dp[i] = dp[i-1] + dp[i-2]`.*
- [ ] 🟡 [House Robber](https://leetcode.com/problems/house-robber/) — *`dp[i] = max(dp[i-1], nums[i] + dp[i-2])`.*
- [ ] 🟡 [Coin Change](https://leetcode.com/problems/coin-change/) — *Fewest coins to make up amount: `dp[a] = min(dp[a - c] + 1)`.*
- [ ] 🟡 [Unique Paths](https://leetcode.com/problems/unique-paths/) — *2D Grid DP: `dp[r][c] = dp[r-1][c] + dp[r][c-1]`.*
- [ ] 🟡 [Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/) — *0/1 Knapsack boolean subset sum.*

#### 🐬 MySQL & Core CS
- **High-Frequency Interview Queries**:
  - Finding duplicate emails: `SELECT email FROM Person GROUP BY email HAVING COUNT(*) > 1;`
  - Self-join comparisons: Finding employees who make more than their direct managers.
  - Simulating conditional logic: `CASE WHEN condition THEN val1 ELSE val2 END`.

#### 🎯 Aptitude: Data Interpretation (Tables & Bar Charts)
- **Approximation Techniques**:
  - Percentage Increase / Decrease: $\frac{\text{Difference}}{\text{Base Value}} \times 100$.
  - When comparing fractions $\frac{A}{B}$ vs $\frac{C}{D}$, cross multiply $A \times D$ vs $B \times C$ instead of doing long division.
- [ ] Solve 3 complete sets on [IndiaBIX Data Interpretation](https://www.indiabix.com/data-interpretation/table-charts/).

---

# 📅 STAGE 3: Synthesis, Weak-Spot Drilling & Mock Tests (Sept 28 – Sept 30)

---

### 📌 Day 14 — Sunday, Sept 28: Heaps, Greedy & Fast Revision

#### 🧠 Concept Deep-Dive & Mental Model
1. **Priority Queue (`heapq`)**:
   - Complete Binary Tree where root is always the minimum element.
   - `heapify`: $O(N)$ linear build.
   - `heappush` and `heappop`: $O(\log N)$.
   - Finding Kth Largest: Keep a min-heap of size $K$. When size exceeds $K$, pop. The root is the $K$-th largest!
2. **Greedy Interval Scheduling**:
   - To accommodate maximum non-overlapping intervals, **sort by END times**. Choosing the interval that ends earliest leaves maximum available time for subsequent intervals.

#### 💻 Direct Coding Practice
- [ ] 🟡 [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) — *Size-K min-heap in $O(N \log K)$.*
- [ ] 🟡 [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) — *`Counter` + `heapq` or Bucket Sort.*
- [ ] 🟡 [Merge Intervals](https://leetcode.com/problems/merge-intervals/) — *Sort by start times and merge overlapping intervals.*
- [ ] 🟡 [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/) — *Greedy sort by end times.*
- [ ] 🟡 [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/) — *2D string matching DP.*

#### 🐬 MySQL & Core CS (Python OOPs)
- **Concept**:
  - 4 Pillars: Encapsulation (naming conventions `_single` and `__double` name mangling), Abstraction (`from abc import ABC, abstractmethod`), Inheritance (Multiple inheritance & Method Resolution Order `ClassName.mro()`), Polymorphism (Duck typing & operator overloading `__eq__`, `__repr__`).
  - `@classmethod` (receives `cls`) vs `@staticmethod` (plain utility in namespace) vs Instance method (receives `self`).

#### 🎯 Aptitude: Data Interpretation (Pie Charts & Caselets)
- **Formulas**:
  - $360^\circ = 100\% \implies 1\% = 3.6^\circ$; $1^\circ = \frac{5}{18}\%$.
  - Convert angles directly into percentages before performing arithmetic.
- [ ] Solve 3 complete sets on [IndiaBIX Pie Charts](https://www.indiabix.com/data-interpretation/pie-charts/).

---

### 📌 Day 15 — Monday, Sept 29: Full Placement Mock Assessment 1

#### 💻 Timed Online Assessment (OA) Simulation 1 (90 Minutes)
- [ ] **Simulated Test Environment (Strict 90 Min Timer)**:
  - Coding Question 1: [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) (Medium)
  - Coding Question 2: [Number of Islands](https://leetcode.com/problems/number-of-islands/) (Medium)
  - 20 MCQs: 10 Aptitude (Syllogisms, Time-Speed, P&C, DI) + 5 MySQL + 5 OS.

#### 🔍 Debrief & Root-Cause Drilling (3.5 Hours)
- [ ] Analyze mistakes:
  - Did you get Time Limit Exceeded (TLE)? Check if you performed $O(N)$ operations in a loop (like `list.pop(0)` or string concatenation).
  - Did any edge case fail (empty string, single node, negative values)?
  - Re-solve missed problems from scratch without viewing solutions.

#### 🐬 Core CS Flash Revision (1.0 Hour)
- [ ] Rapid-fire review of Top 30 OS & MySQL interview questions on GeeksforGeeks / Sanfoundry.

#### 🎯 Aptitude Sectional Drill (1.0 Hour)
- [ ] Take a 30-question mixed timed aptitude mock test on IndiaBIX / Testbook.

---

### 📌 Day 16 — Tuesday, Sept 30: Full Placement Mock Assessment 2 & Final Review

#### 💻 Timed Online Assessment (OA) Simulation 2 (90 Minutes)
- [ ] **Simulated Test Environment (Strict 90 Min Timer)**:
  - Coding Question 1: [3Sum](https://leetcode.com/problems/3sum/) (Medium)
  - Coding Question 2: [Course Schedule](https://leetcode.com/problems/course-schedule/) (Medium)
  - 20 MCQs: Aptitude, MySQL Window Functions, OS Paging & Deadlocks.

#### 🛠️ Final Pattern & Template Consolidation (3.5 Hours)
- [ ] Re-code these 3 foundational algorithms from scratch in under 10 minutes each:
  1. [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)
  2. [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)
  3. [Maximum Subarray (Kadane's)](https://leetcode.com/problems/maximum-subarray/)
- [ ] Review your personal cheat sheet for BFS/DFS, Two Pointers, Monotonic Stack, and Binary Search on Answer.

#### 🐬 MySQL & Resume Polish (1.0 Hour)
- [ ] Review every project bullet point on your resume. Be ready to explain:
  - Why you chose your database schema and architecture.
  - The most difficult bug you resolved and your debugging methodology.

#### 🎯 Aptitude: Final Formula Sheet Review (1.0 Hour)
- [ ] Quick final glance at all formulas: Work-Time LCM, Relative Speed, Syllogism Venn rules, Seating puzzle 2-case setups, P&C selection formulas, and "At Least 1" probability shortcut.

---

## 🏆 Daily Progress Tracker

Mark an `x` as you complete each day's quota:

- [ ] **Day 1 (Sept 15)**: Python Primitives & Math \| Combine Two Tables \| Ratio & Proportion
- [ ] **Day 2 (Sept 16)**: Dicts, Sets & Frequency \| Customers Who Never Order \| Work & Time
- [ ] **Day 3 (Sept 17)**: Recursion & Sorting \| Duplicate Emails \| Pipes & Cisterns
- [ ] **Day 4 (Sept 18)**: Linked Lists from Scratch \| Employees Earning More \| Speed, Distance & Time
- [ ] **Day 5 (Sept 19)**: Stacks & Queues from Scratch \| Second Highest Salary \| Syllogisms
- [ ] **Day 6 (Sept 20)**: Trees & Binary Search \| OS Processes & Scheduling \| Number Series
- [ ] **Day 7 (Sept 21)**: Array Patterns (Kadane's, DNF, 3Sum) \| Delete Duplicate Emails \| Letter Series
- [ ] **Day 8 (Sept 22)**: Binary Search on Answer \| OS Deadlocks \| Case Study: Linear Seating
- [ ] **Day 9 (Sept 23)**: Sliding Window \| Department Highest Salary \| Case Study: Circular Seating
- [ ] **Day 10 (Sept 24)**: LL & Monotonic Stack \| Department Top 3 Salaries \| P&C Part 1
- [ ] **Day 11 (Sept 25)**: Trees & BSTs \| Computer Networks \| P&C Part 2
- [ ] **Day 12 (Sept 26)**: Graphs BFS/DFS \| Consecutive Numbers \| Probability
- [ ] **Day 13 (Sept 27)**: Dynamic Programming \| MySQL Placement Queries \| DI Tables & Bars
- [ ] **Day 14 (Sept 28)**: Heaps & Greedy \| Python OOPs \| DI Pie Charts
- [ ] **Day 15 (Sept 29)**: Full Placement Mock 1 \| OA Debrief \| Mixed Aptitude Drill
- [ ] **Day 16 (Sept 30)**: Full Placement Mock 2 \| Final Code & Formula Consolidation \| Resume Polish
