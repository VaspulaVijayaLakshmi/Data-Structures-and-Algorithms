// [2,3]

// []
// [2]
// [3]
// [2,3]


// Subsets problem

// Output = all intermediate states

// []
// [1]
// [1,2]
// [1,2,3]
// [1,3]
// [2]
// [2,3]
// [3]

// Every recursion state is a valid subset
// → so we do:

// res.push_back(curr);
// at every level
// and not wait till the base condition hits


// Subset Sums problem

// Output = only final sums


// For array [1,2]

// Subsets tree
// []          ← valid
// ├─ [1]      ← valid
// │  └─ [1,2] ← valid
// └─ [2]      ← valid


