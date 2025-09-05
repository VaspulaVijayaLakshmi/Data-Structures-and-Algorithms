907. Sum of Subarray Minimums

Subarray LOgic

// [3,1,2,4]

// [3],          [1],        [2] ,     [4]
// [3,1]        [1,2]        [2,4]     
// [3,1,2]      [1,2,4]
// [3,1,2,4]


// 1 covers till the range on left side 0-1
// 1 covers till the range on right side 3

// so left side means - the subarrays ending at 1
// [......1]

// and rignt side deplicts - subarrays starting from 1
// [1.......]

// and total subarray length in the range  [left - right] 

// Then contribution = arr[i] * left[i] * right[i].

// Step 2. Total subarrays where 1 is the min


// count = leftSpan × rightSpan

// Because:

// Left span = ways to choose starting point of subarray.

// Right span = ways to choose ending point of subarray.


// [3,4,1,2,4]

// [3,4,1]

// so 2 subarrays- [3,4,1]
//                 [4,1]
//                 [1]


// right side - [1,2,4]
//              [1,2]
//              [1]


// IMPortant to handle duplicates:

// Example: arr = [3, 1, 1, 2]

// If both sides used >, then both 1s would try to count the same subarrays → overcount.

// If both used >=, then neither 1 would count some subarrays → undercount.

// With > on left & >= on right → perfect split.

// we should not count subarrays twice. either left side u count of for prev element so this tie no need to expand and count.
