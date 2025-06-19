#LC 350 Problems
https://docs.google.com/spreadsheets/d/1EEYzyD_483B-7CmWxsJB_zycdv4Y5dxnzcoEQtaIfuk/edit?gid=329533698#gid=329533698





# GFG-LEETCODE

This repository contains important DSA questions for Interviews


Pattern Identification/Variations:



https://www.linkedin.com/posts/karan-saxena-466b07190_i-solved-900-leetcode-problems-during-my-activity-7313903802279972864-2IAX/?utm_source=share&utm_medium=member_ios&rcm=ACoAAC4DiGsB5isiUOIm5N4wiyDf3s-QMgXxR-Y




Greedy List

https://www.linkedin.com/posts/karan-saxena-466b07190_greedy-problems-cheatsheet-no-one-told-you-activity-7308116628817231872-L_2-/?utm_source=share&utm_medium=member_ios&rcm=ACoAAC4DiGsB5isiUOIm5N4wiyDf3s-QMgXxR-Y






Pattern Identification/Variations:

https://www.linkedin.com/posts/thecreatorsir_leetcode-coding-programming-activity-7329814345356324866-ELuH/?utm_source=share&utm_medium=member_ios&rcm=ACoAAC4DiGsB5isiUOIm5N4wiyDf3s-QMgXxR-Y


______


BIT MASKING :
https://github.com/VaspulaVijayaLakshmi/Leetcode_FAANG/tree/main/BIT%20MASKING

_____



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

_______________________

EG2: 
Use a set that stores points sorted by x, then y:

bool comparator(pair<int,int> &point1 , pair<int,int> &point2){


   if(point1.first == point2.first)
      return point1.second < point2.second;

      
   return point1.first < point2.first;
      
}

____________________________

EG3 :

1. Sort elements by freq descending ,  if freq is same , then smalleer element should come first

  ( pair<int, int> - freq,int)


bool comparator( pair<int,int> &p1, pair<int,int> &p2 ){

//freq is equal, then smaller element should come first
   if(p1.first == p2.first){
        return p1.second < p2.second;
   }

   else 
   return p1.first >  p2.first;

}

______________

EG4:

SOrt elements by freq descending, and then by lexicograpghically


bool comparator( pair<int,string> &p1, pair<int,string> &p2 ){


if(p1.first == p2.first)
 return p1.second < p2.second;

 return p1.first > p2.first;


}

____________

INTRESTING PROBLEMS:

LC  : 135. Candy - Greedy








https://blog.algomaster.io/p/master-graph-algorithms-for-coding



_______



Never assume details that aren’t explicitly mentioned in the problem statement.

Common clarifications include:

Are there duplicate values?

Can the input be empty? If so, what should the output be?

Should the solution handle negative numbers?

Should the output maintain the original order of elements?

Is the graph directed or undirected?

Does the input contain only lowercase English letters, or can it have uppercase, digits, or special characters?

What should happen if multiple solutions exist? Should I return any valid solution, or does the problem have specific requirements?


___________




BoOk:

https://github.com/VaspulaVijayaLakshmi/Leetcode_FAANG/tree/main/Books


__________




DSU : 



This is imp in prblms like JOB SEQUENCING PROBLEM

BRODEN YOUR HORIZON :



find(x) = "Hey, what's the last free day I can use that’s ≤ x?"
merge(x, x-1) = "Okay, I used day x, so next time don’t return x, return x-1"






