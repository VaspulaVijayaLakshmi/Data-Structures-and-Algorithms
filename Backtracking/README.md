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




