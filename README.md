# GFG-LEETCODE

This repository contains important DSA questions for Interviews


-> N-Queens problem  [Problem link](https://practice.geeksforgeeks.org/problems/n-queen-problem0315/1#)
(https://github.com/VaspulaVijayaLakshmi/GFG-LEETCODE/blob/main/N-queens)


This is the base for next question 
-> Greater on right side  [Problem link](https://practice.geeksforgeeks.org/problems/greater-on-right-side4305/1) <br/>
(https://github.com/VaspulaVijayaLakshmi/GFG-LEETCODE/blob/main/greater%20on%20right%20side)



This become the base for [Raining water Trapping problem](https://www.geeksforgeeks.org/trapping-rain-water/)
(Variations:  Next greater element to right,left)
-> Next Greater Element  [problem link](https://practice.geeksforgeeks.org/problems/next-larger-element-1587115620/1)
(https://github.com/VaspulaVijayaLakshmi/GFG-LEETCODE/blob/main/Next%20Greater%20Element%20to%20right)



-> Rain Water Trapping (https://practice.geeksforgeeks.org/problems/trapping-rain-water-1587115621/1)
[Rain water Trapping Solution](https://github.com/VaspulaVijayaLakshmi/GFG-LEETCODE/blob/main/Trapping%20Rain%20water)


Maximum Subarray Problem  [problem link](https://leetcode.com/problems/maximum-subarray/)
(https://github.com/VaspulaVijayaLakshmi/GFG-LEETCODE/blob/main/maximum%20subarray)






Pattern Identification/Variations:



https://www.linkedin.com/posts/karan-saxena-466b07190_i-solved-900-leetcode-problems-during-my-activity-7313903802279972864-2IAX/?utm_source=share&utm_medium=member_ios&rcm=ACoAAC4DiGsB5isiUOIm5N4wiyDf3s-QMgXxR-Y




Greedy List

https://www.linkedin.com/posts/karan-saxena-466b07190_greedy-problems-cheatsheet-no-one-told-you-activity-7308116628817231872-L_2-/?utm_source=share&utm_medium=member_ios&rcm=ACoAAC4DiGsB5isiUOIm5N4wiyDf3s-QMgXxR-Y






Pattern Identification/Variations:

https://www.linkedin.com/posts/thecreatorsir_leetcode-coding-programming-activity-7329814345356324866-ELuH/?utm_source=share&utm_medium=member_ios&rcm=ACoAAC4DiGsB5isiUOIm5N4wiyDf3s-QMgXxR-Y



Dynamic Programming Patterns: https://lnkd.in/gVNgiDWH

Tree Patterns: https://lnkd.in/gYB7zUX6

Graph Patterns: https://lnkd.in/geZGw4Vt

Substring Problem Patterns: https://lnkd.in/gt23kRen

Backtracking Problem Pattern: https://lnkd.in/gk6JqQD4

Two Pointers Patterns: https://lnkd.in/gfea3T9v

Binary Search Patterns: https://lnkd.in/gHhq5MrR

Cloning Problems Patterns: https://lnkd.in/gJWqTDV8

Bit Manipulation Pattern: https://lnkd.in/gE6cdc-g

Heap Patterns: https://lnkd.in/gugVTJsT

Sliding Window Patterns: https://lnkd.in/gb5NeskQ






2 pointer 

https://www.linkedin.com/posts/mohammadfraz_2-pointer-problems-pattern-cheat-sheet-based-activity-7328764287584296960-WwK5/?utm_source=share&utm_medium=member_ios&rcm=ACoAAC4DiGsB5isiUOIm5N4wiyDf3s-QMgXxR-Y





__________________________________________________________________________________________________________________


Take you forward
Neetcode
Code STory WIth MIK



______________________________________________________________________________________________________________________



Insertion Sort +  Binary Search


This is sometimes called Binary Insertion Sort.

We use Binary Search to find the correct index to insert each element in the sorted portion.
But shifting elements to make space still takes O(n) time.


So Overall Time Complexity of Binary Insertion Sort  -->   

Search: O(log n)
Insert (shift): O(n)
For n elements: O(n × log n) for search + O(n²) for shifting = still O(n²)



________________________________________________________________________________________________________________________



LAZY INSERTION



// Lazy deletion in a heap is a technique used to simulate deletion of elements without immediately removing them from the heap's internal structure.

// Why Use Lazy Deletion?
// Standard binary heaps (like std::priority_queue in C++) do not support efficient removal of arbitrary elements — only the top element (O(log n) for pop,
//  but arbitrary removal is not supported efficiently).

// When you need to delete arbitrary elements (e.g. outdated values in a sliding window), 
// you can use lazy deletion.

// How It Works (Lazy Deletion Strategy):
// Maintain a secondary data structure (e.g., a map or unordered_map) to record how many times an element has been "logically deleted".

// When popping or peeking the top of the heap:

// If the top is marked as deleted (i.e., exists in the delete map), skip it and remove it from both the heap and the delete map.

// Otherwise, it's valid, and you use it.



___________________________________________________________



Custom Comparator Class

A comparator is a function or object that tells the STL how to order two values a and b.


The rule is:

Return true if a should come before b (i.e., a < b in your custom logic).



struct Comparator {

   bool operator()(const Type& a, const Type& b) const {
        return a.property > b.property;  
   
  }
  
};

//This property behaviour can be -> a is less than b, a comes before b, a had less priority  than b

______________________


EG1 : 
Sort words by length, then lexicographically:


bool compareWords(const string& a, const string& b) {

   if (a.length() == b.length())
        return a < b;  // lex smaller first
        
   return a.length() < b.length();  // shorter first
}

sort(words.begin(), words.end(), compareWords);



EG2: 
Use a set that stores points sorted by x, then y:

bool comparator(pair<int,int> &point1 , pair<int,int> &point2){


   if(point1.first == point2.first)
      return point1.second < point2.second;

      
   return point1.first < point2.first;
      
}



EG3:
Prioity_QUEUE

1. Sort elements by freq ,  if freq is same , then smalleer element should come first

  ( pair<intint> - freq,int)


bool comparator( pair<int,int> &p1, pair<int,int> &p2 ){

//freq is equal
   if(p1.first == p2.first){
        return p1.second > p2.second;
   }

   else 
   return p1.first <  p2.first;

}










