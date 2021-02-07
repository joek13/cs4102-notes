---
title: "02. Recurrence Relations"
date: 2021-02-07T10:37:44-05:00
draft: true
---

## Solving recurrence relations
While working on divide and conquer algorithms like MergeSort, we often see runtime formulae that look like:

$$
    T(n) = 2T(\frac{n}{2}) + n
$$

(Recall that this structure arises from how Mergesort splits its input, does some recursive work on either half, and then does some linear work to merge its results.)

On Thursday, we claimed that \\(T(n) \in O(nlogn)\\). Today, we convert this formula to explicit, "closed form."

Four methods for solving:
1. Directly solve
2. Substitution method
3. Recurrence trees
4. "Master" theorem

### Directly solve (unrolling the recurrence)
Solve the "recursed" form by constantly replacing the recursive term into its own value.

$$
    T(n) = 2T(\frac{n}{2}) + n \\
    = 2(2T(\frac{n}{4}) + \frac{n}{2}) + n \\
    = 4T(\frac{n}{4}) + 2n \\
    = 4(2T(\frac{n}{8}) + \frac{n}{4}) + 2n \\
    = 8T(\frac{n}{8}) + 3n \\
    = 2^d * T(\frac{n}{2^d}) + dn
$$

How many times do we have to unroll for $T$ to just equal 1?

Solving for \\(d]\\):
$$
    d = log_2 (n)
$$

In total:
$$
    T(n) = n * 1 + nlogn
$$

Asymptotically, then, \\(T(n) \in \Theta(nlogn)\\).

### "Substitution" method
1. Guess the solution
2. Inductively prove that recurrence is in the proper order class

We guess:
$$
T(n) \le c * n * logn
$$

Choose base case \\(n = 2\\)

$$
    T(2) \le c * 2 * log(2)
    4 \le c * 2log(2)
$$

This is true for \\(c \ge 2\\). Base case holds.

**Inductive step:** Show that \\(Holds(n) \implies Holds(n + 1)\\).

**Conclusion:** Appeal to induction.

### "Recursion tree" method
- Draw the method call as a tree of recursive method calls...
- Figure out how deep the recursion goes, summing the work as you go
- "Draw a picture and count"

Not the best method.... not as rigorous.

### "Master" theorem for D&C
Lets you look at a divide and conquer theorem and come up with one quickly.

Take a recurrence relation:
$$
    T(n) = a T(n/b) + f(n)
$$

f(n) is the "extra work" to combine recursive solution pieces

Then let \\(k = log(a) / log(b) = log_b(a)\\) (critical exponent)

We use \\(n^k\\) as a heuristic for the recursive overhead

Three common cases:
1. If \\(f(n) \in O(n^{k - \epsilon})\\) for some positive \\(\epsilon\\), then \\(T(n) \in \Theta(n^k)\\)
- f is "strictly faster" than the recursion.
- Intuition: if your recursion takes longer than the algorithm itself, the runtime is exactly the recursive overhead.

2. If \\(f(n) \in \Theta(n^k)\\), then \\(T(n) \in \Theta(f(n)logn) = \Theta(n^k logn)\\)
- Intuition: if your recursion and combining take exactly the same time, both play a factor.

3. If \\(f(n) \in \Omega(n^{k + \epsilon})\\) and \\(a * f(n/b) \le c * f(n)\\) for some \\( c < 1\\) and sufficiently large \\(n\\), then \\(T(n) \in \Theta(f(n))\\).
- **Note!!** The _regularity condition_ says that the total work done at the second level of recursion must be strictly upper-bounded by the work done at the top level times some constant.
- f is "strictly slower" than the recursion.
- Intuition: if your recursion takes no longer than the algorithm itself, the runtime is exactly the "combining" overhead.

**Note:** it's possible for none of these cases to hold.