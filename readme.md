# Sorting Algorithms
For the purpose of this module, we will be writing and discussing all sorting algorithms with the assumption that our goal is to sort items in ascending order. But be aware, this does not always have to be the case.

## Day 1 - Why is it so important to sort data?

### We're Always Searching
Users do not have patience for slow apps. And rightfully so! While a a big reason why the applications we use now-a-days are so fast is due to the improvements made in hardware over the last few decades, the software developer still has an important role to play in keeping everything moving quickly.

As we write our applications, we should always be mindful of what operations are being done frequently, since optimizing these will have the biggest impact on the efficiency of our overall application. And regardless of *what* type of app you are creating, it is likely that one of the operations you will be relying on is ***searching***. We search for songs to add to a playlist, videos to watch, people we need to talk to and so much more. Because of this, it is essential that we optimize our searches.

### Linear vs. Binary Search
There are two common searching algorithms that developers are often introduced to when they are writing some of their first apps: linear search and binary search. Let's walk through the differences between them.

#### Linear (Sequential) Search

Sometimes referred to as sequential search, this algorithm is fairly straightforward. Given a set of data, traverse the dataset one item at a time until either you find the item you are looking for OR check every item in the set and verify the item you are looking for is not there.

#### Binary Search

The process of performing a binary search has a couple of extra steps. First, there is a *precondition* that the set of data you are searching is ***already sorted*** (alphabetically, numerically, etc). Then, the steps to search are:

1. Compare the item in the middle of the data set to the item we are searching for.
    - If it is the same, stop. We found it and are done!
    - Else, if the item we are searching for is LESS than the item in the middle:
        - Eliminate the RHS of list. Repeat step 1 with only the LHS of list.
    - Else, the item we are searching for is GREATER than the item in the middle:
        - Eliminate the LHS of list. Repeat step 1 with only the RHS of the list.


A visualization comparing these two algorithms is shown below.
![binary v sequential](https://www.mathwarehouse.com/programming/images/binary-vs-linear-search/binary-and-linear-search-animations.gif "Binary v Sequential Search")

#### Your Task 
- (STRETCH) Complete some of all of the three functions in `searching.py`

#### Runtimes

These two searching strategies have very different runtimes.

**Linear Search:** O(n)  
**Binary Search:** O(log(n))

Looking at the above runtimes, it is clear that we should be using binary search over linear search. 
***However, we cannot perform binary search if our data isn't ALREADY SORTED!***

While the justification for *WHY* we want to sort our data is pretty clear, a harder question to answer is *HOW* do we want to sort our data. Over the next few days, we will explore several different sorting algorithms, examining the pros and cons of each.

[Just for fun...(VIDEO) 15 Sorting Algorithms in 6 Minutes  ![alt text](https://i.ytimg.com/vi/kPRA0W1kECg/maxresdefault.jpg)](https://www.youtube.com/watch?v=kPRA0W1kECg)

## Iterative Sorting Algorithms

### Selection Sort
***Selection Sort*** is an algorithm that many of you have probably used before when sorting things in your everyday lives. Imagine that you have several books you want to arrange on a shelf from shortest to tallest. You start off by looking for the shortest book, and when you find it, put it on the far left side of the shelf. Then, you look for the second shortest book and insert it directly to the right of the first book. You repeat this process, selecting the next shortest book and moving it next to the most recently placed book, until you have moved all books into the right place. This is ***Selection Sort***.  

An example of this algorithm being applied to an array with 10 numerical elements can be seen in the video below.

[(VIDEO) Select-sort with Gypsy folk dance  ![alt text](https://i.ytimg.com/vi/Ns4TPTC8whw/hqdefault.jpg)](https://www.youtube.com/watch?v=Ns4TPTC8whw)


#### Algorithm
1. Start with current index = 0

2. For all indices EXCEPT the last index:

    a. Loop through elements on right-hand-side 
    of current index and find the smallest element

    b. Swap the element at current index with the
    smallest element found in above loop

#### Implementation in Python
```
def selectionSort():
    def selection_sort( arr ):
    # loop through n-1 elements
    for i in range(0, len(arr) - 1):
        cur_index = i
        smallest_index = cur_index
        # find next smallest element
        for j in range(cur_index, len(arr)):
            if arr[j] < arr[smallest_index]:
                smallest_index = j

        # swap
        temp = arr[smallest_index]
        arr[smallest_index] = arr[cur_index]
        arr[cur_index] = temp

    return arr

# try it out
my_arr = [2,5,9,7,4,1,3,8,6]
print(my_arr)
arr = selectionSort(my_arr)
print(my_arr)

```

#### Real-World Applications
While ***Selection Sort*** is one of the easier sorting algorithms to understand and implement, it has one major drawback - its efficiency.

Recall that the runtime complexity of an algorithm, often expressed using *Big O notation*, tells us how the amount of operations our algorithm requires will grow as the size of our input grows. ***Selection Sort*** has  a runtime of O(n²), making it impractical to use with many large, real-world data sets.

#### Your Task
- Complete the missing parts of `selection_sort()` in `iterative_sorting.py` with your instructor

### Insertion Sort
Think back to class or team picture day. Everyone stands in a line facing the photographer. Starting at the left-hand side of the line, the photographer checks to make sure each person is taller than the person next to them. If they are shorter, the photographer pulls them out and shifts people over to the right until he or she finds the right spot for this person. They then insert them back into the line. This process repeats until the photographer reaches the last person on the right-hand side, who must be the tallest person in the group. This is ***Insertion Sort***.

[(VIDEO) Insert-sort with Romanian folk dance  ![alt text](https://i.ytimg.com/vi/ROalU379l3U/hqdefault.jpg)](https://www.youtube.com/watch?v=ROalU379l3U)  

#### Algorithm
1. Separate the first element from the rest of the array. Think about it as a sorted list of one element.

2. For all other indices, beginning with [1]:

    a. Copy the item at that index into a temp variable

    b. Iterate to the left until you find the correct index in the "sorted" part of the array at which this element should be inserted  
    - Shift items over to the right as you iterate
    
    c. When the correct index is found, copy temp into this position

#### Your Task
- Implement the `insertion_sort()` function in `iterative_sorting.py`

```
def insertion_sort():
    # TO BE COMPLETED BY STUDENT

// try it out
arr = [2,5,9,7,4,1,3,8,6];
print(arr);
arr = insertionSort( arr );
print(arr);

```

#### Real-World Applications
The answer to the question, "Is ***Insertion Sort*** an efficient algorithm?" is not always the same. The runtime of ***Insertion Sort*** is dependent on how close to being "in-order" the data is to begin with. In a scenario where you are performing ***Insertion Sort*** on an already or mostly sorted array, very few elements will need to be shifted over, leading to a runtime of Ω(n). However, in a worse-case scenario, where the maximum number of shifts are being performed, the runtime of this algorithm is O(n²).

### MVP
- Complete the missing parts of `selection_sort()` 
- Implement `insertion_sort()`

### Stretch Goals

#### Try to write a search function
- Complete the functions in `searching.py`

#### There are a few "order n" sorting algorithms whose runtime will be linear, even in a worst case scenario. 
Look into Radix Sort and Count Sort.
- How are these algorithms different from other iterative sorting algorithms?
    - What are the advantages/disadvantages to this type of sorting algorithm?
- Take a look a the psuedocode for these algorithms and try implementing one or both of them in Python.

#### You might be surprised what passes for a sorting algorithm
- Explore Bogo Sort and summarize how it works in a couple of sentences.


## Day 2 - A Better Way to Sort

### Divide & Conquer
>A divide-and-conquer algorithm works by recursively breaking down a problem into two or more sub-problems of the same or related type, until these become simple enough to be solved directly.  
-Wikipedia

This approach can be very useful when sorting. By breaking up our original data set into subsets and recursively sorting each subset, we can obtain significant performance gains.

### Recursion Recap
Remember that when writing a recursive algorithm, there are two pieces we have to define:
- Base case
- Recursive case

Recursive cases *must* be written in a way that will eventually allow us to reach the base case. Otherwise, infinite recursion will lead to ***STACK OVERFLOW***!

## Recursive Sorting Algorithms

### Merge Sort
[overview] 

[(VIDEO) Merge-sort with Transylvanian-saxon (German) folk dance  ![alt text](https://i.ytimg.com/vi/XaqR3G_NVoo/hqdefault.jpg)](https://www.youtube.com/watch?v=XaqR3G_NVoo)

#### Algorithm
```
TBC
```
>CHALLENGE: One implementation is shown below, but take a stab at writing the code for this yourself before scrolling down!

#### Implementation in Python
```
def mergeSort():
    //TBC

// try it out
var arr = [2,5,9,7,4,1,3,8,6];
print( "Unsorted array: " + arr);
arr = mergeSort( arr );
print( "Sorted array: " + arr);

```

#### Real-World Applications
Have you ever wondered how some of the languages you use actually implement their built-in `sort()` functions? Many of them actually utilize the ***Merge Sort*** algorithm! 

#### Check for understanding
1. TBD
    <details><summary>Answer</summary> ... </details>

2. When using ***Merge Sort***, what is the difference between the order or arrangement of elements in *best case* versus *worst case*?
    <details><summary>Answer</summary> ... </details>

3. When using ***Merge Sort***, what would be the runtime of sorting elements in the best, average, and worst cases?
    <details><summary>Answer</summary>
    <ul><li>Best case:    O(nlog(n))</li>
    <li>Average case: O(nlog(n))</li>
    <li>Worst case:   O(nlog(n))</li>
    </details>

4. Show how the array **[4, 8, 3, 1, 9, 6]** changes as it is being sorted using ***Merge Sort***. To do this, write out the contents of the array after each pass of the algorithm. (_hint...we should only need n-1 passes to sort the array, where n is the size_)
   <details><summary>Answer</summary> <pre><samp>           [4, 8, 3, 1, 9, 6]       // divide
                /            \
          [4, 8, 3]       [1, 9, 6] 
            /     \         /     \
         [4, 8]   [3]    [1, 9]   [6] 
         /    \    |     /    \    |
        [4]   [8] [3]   [1]   [9] [6]   // merge
         \    /    |     \    /    |
         [4, 8]   [3]    [1, 9]   [6]
           \      /       \       /
          [3, 4, 8]       [1, 6, 9]
              \               /
              [1, 3, 4, 6, 8, 9] </samp></pre></details>

### Quick Sort
[overview] 

[(VIDEO) Quick-sort with Hungarian folk dance  ![alt text](https://i.ytimg.com/vi/ywWBy6J5gz8/hqdefault.jpg)](https://www.youtube.com/watch?v=ywWBy6J5gz8)


#### Algorithm
```
TBC
```

#### Implementation in Python
```
def quickSort():
    // TBC


// try it out
var arr = [2,5,9,7,4,1,3,8,6];
print( "Unsorted array: " + arr);
arr = quickSort( arr );
print( "Sorted array: " + arr);

```

#### Real-World Applications
While ***Quick Sort*** has "quick" in its name, it is typically not used as frequently as Merge Sort. Although it *is* quick in a best case scenario, worst case for ***Quick Sort*** is *very* bad. Because of this, it is not often chosen for production.

#### Check for understanding
1. In ***Quick Sort***, if the leftmost element of an already sorted array is chosen as the pivot, this leads to worst case performance. Explain why.

2. Consider a scenario in which you have _____. Which recursive sorting algorithm would you chose and WHY?


3. When using ***Quick Sort***, what would be the runtime of sorting elements in the best, average, and worst cases?
    <details><summary>Answer</summary>
    <ul><li>Best case:    O(nlog(n))</li>
    <li>Average case: O(nlog(n))</li>
    <li>Worst case:   O(n²)</li>
    </details>

4. Show how the array **[4, 8, 3, 1, 9, 6]** changes as it is being sorted using ***Quick Sort***. To do this, write out the contents of the array after each pass of the algorithm. (_assume the pivot will be the middle index, mid=len of subarray / 2_)
   <details><summary>Answer</summary> <pre><samp>[1, 8, 3, 4, 9, 6]  // pivot = 1  
   // Quick Sort LHS, RHS of 1
   [1, 8, 3, 4, 9, 6]  // LHS done ✓
    ✓             
   [1, 8, 3, 4, 9, 6]  // RHS pivot = 4
    ✓                
   [1, 3, 4, 8, 9, 6]  
    ✓             
   // Quick Sort LHS, RHS of 4
   [1, 3, 4, 8, 9, 6]  // LHS done ✓
    ✓  ✓  ✓  
   [1, 3, 4, 8, 9, 6]  // RHS pivot = 9
    ✓  ✓  ✓     
   [1, 3, 4, 8, 6, 9]  
    ✓  ✓  ✓        
   // Quick Sort LHS, RHS of 9
   [1, 3, 4, 8, 6, 9]  // RHS done ✓
    ✓  ✓  ✓        ✓
   [1, 3, 4, 8, 6, 9]  // LHS pivot = 6
    ✓  ✓  ✓        ✓
   [1, 3, 4, 6, 8, 9]  
    ✓  ✓  ✓        ✓
   // Quick Sort LHS, RHS of 6
   [1, 3, 4, 6, 8, 9]  // LHS, RHS done ✓
    ✓  ✓  ✓  ✓  ✓  ✓</samp></pre></details>

### Stretch Goals

#### Tim Sort is a combination of the Merge Sort and Insertion Sort algorithms.
- What programming languages use **Tim Sort** to implement their built-in `sort()` functions?
- If an interviewer asked you to describe the **Tim Sort** algorithm in 3-4 sentences, what would you say?
- Can you implement **Tim Sort** in Python?
