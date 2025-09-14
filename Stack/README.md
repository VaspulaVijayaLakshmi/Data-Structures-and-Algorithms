*** IMP STACK 

# Subarray Tricks

## 907. Sum of Subarray Minimums

arr = [0,3,4,5,2,3,4,1,4]


- `0` contributes to all subarrays starting with `0`.

- `3`:  
  - Left side: no contribution (since `0` is smaller).  
  - Right side: contributes to `[3]`, `[3,4]`, `[3,4,5]`.  

- `4`:  
  - Left side: none.  
  - Right side: `[4]`, `[4,5]`.  

- `2`:  
  - Left side: `[3,4,5,2]`.  
  - Right side: `[2]`, `[2,3]`, `[2,3,4]`.  

---

## How to Find Contribution

We need:

- **Next smaller element to the left**  
- **Next smaller element to the right**

We can calculate this using a **monotonic stack**.




## Duplicates Handling

Example:  
arr = [3,1,1,2]



If both sides used `>` → both `1`s would count the same subarrays (**overcount**).  
If both used `>=` → some subarrays would not be counted (**undercount**).  

Correct way:  
- Use `>` for **left**  
- Use `>=` for **right**

This avoids double counting.








# Subarray Minimum Contribution

We need to find the **minimum element** in subarrays and see how many subarrays it contributes to where it is the minimum.

---

## Example 1
arr = [3,1,2,4]



We want to check each element’s contribution:

[3], [1], [2], [4]
[3,1], [1,2], [2,4]
[3,1,2], [1,2,4]
[3,1,2,4]




- `1` covers till the range on the left side: indices `0–1`.  
- `1` covers till the range on the right side: index `3`.  

**Left side** → subarrays ending at `1` → `[...1]`  
**Right side** → subarrays starting from `1` → `[1...]`  

Total subarray count in the range = `left × right`  



**Contribution**:  
arr[i] × left[i] × right[i]





__________________________________


## 2104. Sum of Subarray Ranges
https://leetcode.com/problems/sum-of-subarray-ranges/description/

# Similar to above.

// For each element, find:
// Previous Smaller or Equal Element (PSEE) and Next Smaller Element (NSE) → counts contribution as minimum.
// Previous Larger or Equal Element (PLEE) and Next Larger Element (NLE) → counts contribution as maximum.
// Multiply contributions accordingly and sum them.



So each element we need to check - how many subarray

MIN: 
->  subarrays ending at this elemnt where this is the min element
->  subarrays starting at this element where this is the min element

-> this basically boils down to -> next smaller element to left and right.



MAX :
->  subarrays ending at this elemnt where this is the max element
->  subarrays starting at this element where this is the max element

-> next larger lement right and left.

___________


//now how mnay contributions : 


so when we do this, we cover the 


// The final answer = sum of maximum contributions – sum of minimum contributions.  ?????????????///
