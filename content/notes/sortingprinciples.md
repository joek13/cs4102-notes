---
title: "01. Sorting and Some Algorithm Principles"
date: 2021-02-02T20:36:51-05:00
draft: true
---

### Introduction: Sorting
Given: a sequence of items \\(a_0 \dots a_n \\),

Task: reorder sequence to permutation \\(a'\\) s.t. \\( a'\_i \\le a\_{i+1} \\) for all pairs.
(Sorting in "non-descending" orders.)

Restriction: we're looking at algorithms that sort using key comparisons. Our *basic operation* for runtime analysis will be a comparison of two items' key-values.
Why?
- It's general
- Controls number of other operations 
- The logic of the comparison itself could be expensive for, say, long strings

#### Some observations
- We assume non-descending order for simplicity
- Our analysis results generalize to other orderings, in practice we can use a comparison function (e.g., Java's `Comparable`)

### Terminology
Comparison sort: only compares and move items

Adjacent sort: algorithms that sort by only swapping adjacent elements

Stable sort: a sorting algorithm is stable ↔ when two items x and y occur in the relative order x,y in the original list AND x == y, then x and y appear in the same relative order in the final sorted list

In-place sort: the algorithm uses at most \\( \Theta(1) \\) extra space
- e.g., allocating a second "scratch" array is not allowed

### Why study sorting?
It's an important problem, and underpins many other algorithms

It's also useful for the study of algorithms:
- History of sorting algorithms
- Illustrates various design strategies
- Illustrates analysis methods
- Illustrates how we prove optimality
    - Proved in the live section...

## Insertion sort
Strategy:
1. First section of list is sorted
2. Increase the partial solution by:
3. Shifting down next item beyond sorted section down to its proper place in sorted section. (Must shift items to make room for new element.)
4. Since one item alone is already sorted, we can put steps 1-3 in a loop going from second to last item.

Exemplifies a general strategy; we extend a partial solution by increasing its size by one. Some call this "*decrease and conquer*"

### Proving it right: loop invariants
An important technique for proving algorithm correctness.

Properties that hold true at these points:
- Prior to first iteration (initialization)
- If true before an iteration, then it's true after that iteration (maintenance)
- When loop ends, properties still hold (termination)

Loop invariant for insertion sort:
> For the for-loop governed by index j, the values `A[0..j-1]` are the elements originally stored in the sublist but in sorted order.

### Properties of insertion sort
- Easy to code
- In-place sort
- What's it like if the list is sorted? Or almost sorted?
- Fine for small inputs. Why? (No recursive overhead)
- Stable

### Analysis
Worst-case:
$$
    W(n) = \sum_{j=2}{n}{(j-1)} = \frac{1}{2}(n)(n-1) \in \Theta(n^2)
$$

Average behavior (messy and ugly):
$$
    \text{Lotsa math} \approx \frac{1}{4}n^2
$$

Best-case:
$$
    B(n) = \sum_{j=2}^{n}{1} = n-1
$$
Interesting note: the best-case behavior does exactly as much work as is necessary to *check* something is sorted....🤔 

### Insertion sort: "best of a breed"
We know that insertion sort is one of many quadratic sort algorithms, and that loglinear sorts do exist

But can we learn something about insertion sort that tells us what it is about the algorithm that "keeps" it in the slower class.

Yes: we use a lower-bounds argument for adjacent sort algorithms

Sorting a list by only swapping adjacent elements is \\(\Theta(n^2)\\) and can never be \\(o(n^2)\\)

#### The lower-bounds argument for adjacent sorts
We define _inversions_ as a pair of elements (not necessarily adjacent) that are misordered.
Sorting, then, can be viewed as a process to remove inversions.

Note about adjacent sorts: one swap will only ever remove one inversion.

Question: what's the maximum number of inversion we can have in a list of size \\(n\\)?

Answer: \\(\frac{n(n-1)}{2}\\)

**Theorem.** Any algorithm that sorts by comparison of keys and removes at most one inversion after each comparison must do at least \\(\frac{n(n-1)}{2}\\) comparisons in the worst case.

This theorem applies to any adjacent sort. Result: the optimal worst-case time complexity of an adjacent sort is \\(\Theta(n^2)\\)

## Mergesort, Divide & Conquer
General and practical sorting algorithm

### Divide and conquer strategy
Has following "general structure"
```
solveProblem(input):
    if input is small:
        solve directly (brute force?)
    else:
        divide problem into n smaller problems
        recursively invoke solveProblem on smaller problems
        combine solutions into bigger solution
        return bigger solution
```

Runtime of a divide-and-conquer algorithm is the sum of the times to divide, recursively solve, and combine

### Mergesort as Divide & Conquer
- Base case:
    - sublist is size 1, already sorted
- Divide:
    - Divide list into two sublists of equal size
- Conquer:
    - Call mergesort recursively on each sublist
- Combine:
    - Merge sorted left sublist and sorted right sublist

Most of the work gets done in `merge()`:
- Comparisons, moves
- Most implementations use a "scratch array"
    - An array of size \\(n\\) which is copied into

The problem for `merge()`:
- Given two sorted sequences A and B, merge them to create one sorted sequence C

Strategy:
- C is initially empty
- Look at the first (current) items in A and B
- The smallest of these should become the next item in C
- Go to 2
- When you've exhausted one list, simply append the other list's outstanding items to C

Time complexity: \\(\Theta(n)\\)

Runtime, T(N):
- Divide the list: \\(\Theta(1))\\)
- Two recursive sorts: each costs \\(T(n/2)\\)
- Merge: linear, \\(\Theta(n)\\)

Overall cost:
$$
    T(n) = 2T(n/2) + n = \Theta(nlog(n))
$$

Why??? Just wait.... 