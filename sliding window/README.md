https://leetcode.com/problems/frequency-of-the-most-frequent-element/solutions/1175088/C++-Maximum-Sliding-Window-Cheatsheet-Template/


Also the number of subarrays formed from [l.....r]

r-l+1



//  0  1
// [10,5] k =55

// [10] [5] [10,5]

// [10]         - res = 0-0+1 = 1
// [10,5].      - res = 1-0+1 = 2


// so its 3
