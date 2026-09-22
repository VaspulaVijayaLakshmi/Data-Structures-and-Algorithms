# Backtracking: Subsets vs Subset Sums

## 1. Subsets Problem

### Key Idea

**Every recursion state is a valid subset.**

Therefore, we add the current state to the result **at every recursion level**:

```cpp
res.push_back(curr);
```

We do **not** wait for the base condition.

### Example

For:

```text
[1, 2, 3]
```

Output:

```text
[]
[1]
[1,2]
[1,2,3]
[1,3]
[2]
[2,3]
[3]
```

### Recursion Tree

```text
[]                  ← valid subset
├── [1]             ← valid subset
│   ├── [1,2]       ← valid subset
│   │   └── [1,2,3] ← valid subset
│   └── [1,3]       ← valid subset
│
├── [2]             ← valid subset
│   └── [2,3]       ← valid subset
│
└── [3]             ← valid subset
```

### Pattern

```cpp
void dfs(int start) {

    res.push_back(curr);  // every state is an answer

    for (int i = start; i < n; i++) {

        curr.push_back(nums[i]);

        dfs(i + 1);

        curr.pop_back();
    }
}
```

---

# 2. Subset Sums Problem

### Key Idea

Here, we don't need to store every intermediate subset.

We only need the **final sum for each subset**.

For:

```text
[1, 2]
```

Subsets:

```text
[]
[1]
[2]
[1,2]
```

Subset sums:

```text
0
1
2
3
```

### Pattern

```cpp
void dfs(int index, int sum) {

    if (index == n) {
        res.push_back(sum);  // only final states
        return;
    }

    // Take
    dfs(index + 1, sum + nums[index]);

    // Don't take
    dfs(index + 1, sum);
}
```

---

# Important Difference

| Problem | What is an answer? | When do we add to result? |
|---|---|---|
| **Subsets** | Every intermediate state | Every recursion level |
| **Subset Sums** | Final sum of each subset | At base condition |

### Remember

```text
Subsets
→ Every state is an answer
→ res.push_back(curr) at every level

Subset Sums
→ Only completed subset matters
→ res.push_back(sum) at base condition
```


---


# Backtracking Pattern: "Put a Mark at Every Position"

A useful way to recognize backtracking problems:

> **If I can put a separator / mark / cut at different positions, use a `for` loop to try every possible position.**

---

## 1. Core Idea

Suppose we have:

```text
"aab"
```

We want to partition it.

From `start = 0`, possible cuts are:

```text
a | ab
aa | b
aab |
```

Instead of manually placing a mark at every position, use:

```cpp
for (int j = start; j < n; j++)
```

Each `j` represents one possible place where the current piece ends.

```text
j = 0 → s[start...0] = "a"
j = 1 → s[start...1] = "aa"
j = 2 → s[start...2] = "aab"
```

---

# 2. General Pattern

```cpp
void dfs(string& s, int start) {

    for (int i = start; i < s.size(); i++) {

        // Choose s[start...i]

        if (!isValid(start, i))
            continue;

        // Make choice
        curr.push_back(s.substr(start, i - start + 1));

        // Solve remaining part
        dfs(s, i + 1);

        // Undo choice
        curr.pop_back();
    }
}
```

Think:

```text
start
  |
  |--- choose [start...i]
  |
  |--- recurse from i+1
  |
  |--- undo
```

---

# 3. Palindrome Partitioning

For:

```text
aab
```

At `start = 0`:

```text
j = 0 → "a"   ✓
j = 1 → "aa"  ✓
j = 2 → "aab" ✗
```

If `"a"` is chosen:

```text
a | ab
    ^
    start = 1
```

Now again try every possible ending:

```text
a | b
ab
```

This gives:

```text
a | a | b
```

If `"aa"` is chosen:

```text
aa | b
```

Final result:

```text
["a","a","b"]
["aa","b"]
```

---

# 4. The Important Mental Model

Don't think:

```text
"I need to manually put a separator."
```

Think:

```text
"Where can my next piece END?"
```

Then:

```cpp
for (int i = start; i < n; i++)
```

tries every possible ending.

So:

```text
FOR LOOP
   ↓
tries every possible cut
   ↓
validate the chosen piece
   ↓
recurse on remaining string
   ↓
backtrack
```

---

# 5. Why `start` Is Important

`start` tells us:

> **Where the unprocessed part begins.**

Example:

```text
a | ab
    ↑
  start = 1
```

We don't reconsider the `"a"` we already selected.

We only partition:

```text
"ab"
```

Hence:

```cpp
dfs(i + 1);
```

---

# 6. Where This Pattern Appears

### Palindrome Partitioning

```text
aab

a | ab
aa | b
aab
```

The loop chooses where the next palindrome ends.

### Restore IP Addresses

```text
25525511135

255 | 255 | 11 | 135
```

The loop chooses where the next IP segment ends.

### Word Break / String Partitioning

```text
leetcode

leet | code
```

The loop chooses where the next word ends.

### General Partition Problems

Whenever you see:

> "Split the string/array into multiple parts."

Ask:

> **"Where can the next part end?"**

Then consider:

```cpp
for (int i = start; i < n; i++)
```

---

# 7. Universal Pattern

```cpp
for (int i = start; i < n; i++) {

    // choose [start...i]

    if (!valid(start, i))
        continue;

    curr.push_back(...);

    dfs(i + 1);

    curr.pop_back();
}
```

### One-line memory trick

> **Partition problem → `for` loop represents the possible cut positions.**

The loop is essentially your **"mark at every position"** idea implemented cleanly.

