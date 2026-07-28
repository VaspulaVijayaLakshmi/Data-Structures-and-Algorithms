In subarray problems we have sometimes -> use mp[0]=0 or mp[1]=1 or mp[0]=-1

This is a very important distinction. 
The confusion happens because mp[0] means different things depending on what you are storing in the map.



1️⃣ When map stores index → mp[0] = -1

Example: Longest Subarray with Sum K

unordered_map<int, int> mp;
mp[0] = -1;

Here the map is:
prefix sum → index

0 → -1 means:
Prefix sum 0 occurred before the array started, at index -1.



2️⃣ When map stores frequency → mp[0] = 1

Example: Count Subarrays with Sum K

unordered_map<int, int> mp;
mp[0] = 1;

Here the map is:
prefix sum → frequency

0 → 1 means:
Prefix sum 0 has occurred once before the array starts.



_______________________________________________________________



If map stores an INDEX:
prefix sum → index

Use:

mp[0] = -1;

Because you're saying:
"The prefix sum 0 exists at index -1."




If map stores a COUNT/FREQUENCY:
prefix sum → frequency

Use:

mp[0] = 1;

Because you're saying:
"The prefix sum 0 has appeared once."

