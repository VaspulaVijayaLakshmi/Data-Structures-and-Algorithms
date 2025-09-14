907. Sum of Subarray Minimums


# Subarray Minimum Contribution

This document explains how to calculate the contribution of each element in an array to all subarrays where it is the **minimum element**.  

---

## Problem Statement

Given an array, for each element we want to find:

- How many subarrays exist where this element is the minimum.  
- The contribution of that element to the total sum of subarray minimums.

---

## Example Walkthrough

### Example 1:  
arr = [3, 1, 2, 4]

css
Copy code

All possible subarrays:
[3], [1], [2], [4]
[3,1], [1,2], [2,4]
[3,1,2], [1,2,4]
[3,1,2,4]

markdown
Copy code

Now, check contribution:

- `1` is the minimum in **all subarrays containing it** except when another smaller element appears.  
- We calculate its contribution using **left span** and **right span**.

---

## Concept

For each element `arr[i]`:

- **Left span** = Number of choices for starting index of subarray where `arr[i]` is min.  
- **Right span** = Number of choices for ending index of subarray where `arr[i]` is min.  

So,  

count[i] = leftSpan[i] × rightSpan[i]
contribution[i] = arr[i] × count[i]

yaml
Copy code

---

## Using Monotonic Stack

We use stacks to efficiently find:

- **Next smaller element on the left (NSL)**
- **Next smaller element on the right (NSR)**

This gives us the span of influence for each element.

---

### Example 2:  
arr = [0, 3, 4, 5, 2, 3, 4, 1, 4]

markdown
Copy code

- `0`: Contributes to all subarrays starting with `0`.  
- `3`:  
  - Left side: No contribution (blocked by `0`).  
  - Right side: `[3]`, `[3,4]`, `[3,4,5]`.  
- `4`:  
  - Left side: None.  
  - Right side: `[4]`, `[4,5]`.  
- `2`:  
  - Left side: `[3,4,5,2]`.  
  - Right side: `[2]`, `[2,3]`, `[2,3,4]`.  

---

## Handling Duplicates

When array has duplicates:  

Example:  
arr = [3, 1, 1, 2]

markdown
Copy code

- If both NSL and NSR use `>` → double count subarrays.  
- If both use `>=` → undercount subarrays.  
- **Correct rule:**  
  - Use `>` for **NSL**.  
  - Use `>=` for **NSR**.  

This ensures each subarray is counted **exactly once**.

---

## Final Formula

For each element `arr[i]`:

contribution[i] = arr[i] × leftSpan[i] × rightSpan[i]

yaml
Copy code

Where:

- `leftSpan[i] = i - NSL[i]`
- `rightSpan[i] = NSR[i] - i`

---

👉 This forms the basis of the **Sum of Subarray Minimums** problem. 








