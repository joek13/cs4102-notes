---
title: "00. Syllabus Day"
date: 2021-02-01T15:23:56-05:00
draft: true
---

Slides are hosted on [the course website](https://uva-cs.github.io/cs4102-s21/readme.html).

Office hours are hosted on the class Discord.

## The textbook
We "really need" to read and study material from the textbook.
Readings are posted as assigned, and the textbook can be accessed for free from the UVa Library.

## Modules
The course is divided into four modules.
1. Divide and conquer / sorting
2. Graphs, MST, find-union
3. Greedy algorithms and dynamic programming
4. Network flow and reductions

## Quizzes
Short assessments for each of the four modules.
- Will be take-home over a ~24 hour period

Three possible grade outcomes: incomplete, satisfactory, mastered. You'll have three opportunities at most of these.

## Homeworks
Two kinds: most homeworks are programming assignments or written descriptions of algorithms / proofs

### Programming HW
- Can be written in Java, C++, Python
- Almost HackerRank style problems

### Written HW
- Solving small problems, analyzing runtimes, etc.
- Proofs of correctness, etc.
- Typeset in LaTeX

Homeworks are also graded according to completeness. Homeworks can be submitted multiple times.

Homeworks have two deadlines: soft and hard. Soft deadlines are scheduled several days before quizzes, so you're best prepared. But the hard deadline is almost two weeks later. There is no grade penalty for missing the soft deadline.

### Programming homework
Some tips:
- Understand the problem; hidden test cases are used for grading
- Consider all boundary cases
- Use pre-existing library code
- Know how to handle floating point numbers

### Typesetting
Templates and tutorials are provided. Including images of text or formulas is verboten!

## Collaboration
Quizzes are strictly independent.

Programming homeworks can be completed in groups of 3 or fewer to discuss the algorithmic aspects only.
(Credit your co-conspirators using a comment in your code.)

Written homeworks can be completed in groups of 3 or fewer, but you have to type up your own solution.

## Academic integrity
Collaboration is allowed and encouraged.

Do not:
- Share written solutions
- Share documents (e.g., with Overleaf)
- Share debugging of code
- Seek published solutions online

Do:
- Be able to explain anything you submit.

### What you already know from CS2150
- Definition of an algorithm
- Definition of algorithm complexity
- Measuring worst-case complexity
- Cost as a function of input size
- Asymptotic growth rate: \\( O \\), \\( \Theta \\)

### What you already know from 2102/3102
- Proof by induction, contradiction
- Counting, probability, combinatorics, permutations

## Introducing an algorithm
### A first algorithm: making change
Problem: given item cost, and amount paid, make change *(using the fewest possible coins)*.

E.g.: Costs $4.37, paid $5 → two quarters, a dime, and three pennies

Solution: look at outstanding amount; while it's greater than zero, take the largest coin value that's less than the amount oustanding, add it to the change, and subtract its value.

Q: Is this solution optimal? How could we show this?
A: Prove that it's *impossible* to solve this more efficiently.

### Greedy algorithms
Example of a family called *greedy algorithms*

Suitable for optimization problems: class of problems with many feasible solutions, but only one is optimal

Immediately greedy: at each step, choose the "best" solution for right now. Don't look into the future.

For some optimization problems, greedy algorithms are great; for others (e.g. select the best cheess move), they aren't.

Interesting note: our greedy algorithm is only best for American coins. For example: say we had an 11-cent coin (the Floryan), making change for 15 cents.

Our algorithm says: `1 Floryan, 4 pennies`. But a better solution exists: `1 dime, 1 nickel`.

Can we come up with a change algorithm that generalizes better? There are a few approaches:
- Brute force
- Dynamic programming