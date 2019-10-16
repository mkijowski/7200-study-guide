# CS 7200 Midterm Exam Guide
This guide will be made as a study tool for the first exam.  I will primarily be
using it to force myself to find and read the linked materials, and I would
recommend other students do the same, but feel free to use this as a reference
(please do not blame me for any grades earned by using this guide as a sole
reference)!

I will be starting this guide by documenting 2 things, the email sent
describing what will be on the exam, and the practice midterm on Dr. Prasad's
site.

[My solutions to the 2013 midterm
provided.](https://github.com/mkijowski/7200-study-guide/blob/master/README.md#sample-midterm)

Here are the topics TK says will be on the exam:
1. [Stable Marriage (15
   pts.)](https://github.com/mkijowski/7200-study-guide/blob/master/README.md#stable-marriage)
   * perfect and stable matching
   * ability to derive stable match
2. [Big 0 notation (10
   pts.)](https://github.com/mkijowski/7200-study-guide/blob/master/README.md#big-o-notation)
   * in line with assignment problem
   * given a number of functions
3. [Analysis of loops (5
   pts.)](https://github.com/mkijowski/7200-study-guide/blob/master/README.md#analysis-of-loops)
   * provided a nested loop, summarize number of iterations in Big-O notation
4. [Trees
   (5pts.)](https://github.com/mkijowski/7200-study-guide/blob/master/README.md#trees)
   * Some basic questions on binary trees at the introductory level
5. [Algorithm Design (?
   pts.)](https://github.com/mkijowski/7200-study-guide/blob/master/README.md#algorithm-design)
   * Define a problem similar to one in class (probably a greedy algorithm)
   * Provide a heuristic for solving it
   * We will write pseudo-code for the algorithm
   * We will prove if the heuristic generates an optimal solution or provide a
     counter-example if not
6. [Divide and
   conquer (? pts.)](https://github.com/mkijowski/7200-study-guide/blob/master/README.md#divide-and-conquer)
7. [Recursive tree and Master Theorem( ?
   pts.)](https://github.com/mkijowski/7200-study-guide/blob/master/README.md#recursive-tree-and-master-theorem)
   * be able to identify what the master theorem is
   * identify when master theorem applies
   * is master theorem does not apply be able to apply recursive tree

## Stable Marriage
[Best described on Wikipedia][1]. The Stable Marriage Problem (also called
**Stable Matching Problem** or **SMP**) is the problem of finding a stable 
matching between two equally sized sets of elements given an ordering of 
preferences for each element. A matching is a mapping from the elements of one 
set to the elements of the other set.  A match is *not* stable if:
```
  1. There is an element A of the first matched set which prefers some given 
     element B of the second matched set over the element to which A is already 
     matched, and
  2. B also prefers A over the element to which B is already matched
```

#### Gale-Shapley algorithm
The Gale-Shapely algorithm is one solution to such a problem that will always
produce a stable match.  Also called the **Deferred Acceptance** algorithm,
Gale-Shapley initializes all elements (men and women) to be free.  The algorithm
then iterates over a number of rounds.

In the first round each man proposes to the woman he prefers most, and each
woman replies with a "maybe" (*deferred acceptance*) to her most preferred
suitor and a "no" to all other suitors.  She is then provisionally engaged to
her suitor, and her suitor is likewise provisionaly engaged to her.

In each subsequent round each unengaged man proposes to the most preferred woman
that he has not yet proposed (regardless of whether that woman is engaged or
not).  Each woman replies "maybe" if she is not currently engaged **or** if she
prefers this man over her current provisional partner, when then becomes
unengaged.

These iterations finish once everyone is engaged.  The algorithm allows women to
"trade up" and in the process jilt her until-then partner.

##### The algorithm guarantees that:

###### Everyone gets married
At the end there cannot be a man and woman both unengaged since he at some point
must have proposed to her and she would have provisionally accepted.

###### The marriages are stable
Let Alice and Bob both be engaged, but not to each other. Upon completion of the 
algorithm, it is not possible for both Alice and Bob to prefer each other over 
their current partners. If Bob prefers Alice to his current partner, he must 
have proposed to Alice before he proposed to his current partner. If Alice 
accepted his proposal, yet is not married to him at the end, she must have 
dumped him for someone she likes more, and therefore doesn't like Bob more 
than her current partner. If Alice rejected his proposal, she was already 
with someone she liked more than Bob.

##### Algorithm
```
function stableMatching {
    Initialize all m ∈ M and w ∈ W to free
    while ∃ free man m who still has a woman w to propose to {
       w = first woman on m's list to whom m has not yet proposed
       if w is free
         (m, w) become engaged
       else some pair (m', w) already exists
         if w prefers m to m'
            m' becomes free
           (m, w) become engaged 
         else
           (m', w) remain engaged
    }
}
```

##### Some things to consider
* There can be multiple stable matchings
* The above algorithm optimizes for men, not women
* The algorithm can be inverted for women to propose to men and men defer
  acceptance until all are engaged
* ??? The algorithm above will always return the same stable matching for the same
  ordering of inputs (if you want a different matching you need to scramble the
  order in which you allow men to propose).  **Can I prove/show this to be true???**

### Big-O Notation
Similar to assignment question.  Given a series of functions, order them based
on increasing/decreasing growth rate.

When comparing two equations, start by reducing them as much as possible.
Ignore all constants and lower order terms.  Then apply the below.

Basic Big-O hierarchy:
```
O(1) < O(log[n]) < O(n) < O(n*log[n]) < O(n^x) < O(x^n) < O(n!)
```

## Analysis of loops
* Loop variable incremented by a constant amount requires `O(n)` time.
* Complexity of nested loops is `O(n^c)` which is the number of times the
  innermost statement is executed.  One nested loop would be n^2 time, two nested
  loops n^3 and so on.
* If the loop variable is multiplied or divided by a constant amount the time
  complexity is `O(log n)`
* If the loop variable is incremented/decremented exponentially by an amount the
  time complexity is `O(log log n)`

Combining time complexities of consecutive loops simply sum the time complexity
of each individual loop.

## Trees
Trees are simply undirected graphs that contain no cycles.
* describe and implement heap
* Know trees, binary, three-ary, be able to figure out depth of trees


## Algorithm Design

* algorithm design, variant of something we've already seen (greedy algorithm)
* algorithm design / pseudo code similar to assignment
  * sort, walk thorugh, collect or not collect

## Recursive tree and Master Theorem

#### Deriving Master Theorem (and possibly Muster)
* First, learn the recursion tree method. Learn how to build the tree, how to count the number of leaves, and how to count the amount of "extra work" at each level, and how to sum them (by summing a series, e.g., a geometric series).
* Next, open up a textbook read a standard proof of the Master theorem. Work through each step and check that you understand what's happening.
* Now, close your textbook and put away all your resources. Put a blank piece of paper in front of you... and derive the Master theorem yourself. How do you do that? Well, you use the recursion tree method. Try working through it by yourself and try to solve the recurrence entirely on your own. If you get stuck, as a last resort you can open the textbook back up and see how to proceed from there... but then the next day, you should try this exercise again.


master theorem is comparing the effort between the recursive splitting step
(divide and combine), and the solution effort of the simplest case.

fourth condition to Master theorem is applied in the closest point algorithm

fibonacci sequence special case
tower of hannoi special case (guess and prove or muster theorem)

its not that master theorem doesnt apply to non-polynomial functions, we just
cant prove that it does apply

## Sample Midterm
###### 1) [Stable  Marriage  Problem]
State  whether  the  following  claims  are true  or false.   
If   true,   justify it as   clearly   as   possible. If false, provide a 
counterexample/argument.

``` 
(a) If w is the top choice of m, and m is the top choice of w, then m and w 
    must be paired with each other in any stable matching.
```

My answer is this is true.  Consider the first proposal of *m*.  Since *w* is
*m*'s top choice, she is propsed to first and if she is not engaged the proposal 
is conditionally accepted.  If she is ingaged because *m* is her top choice she
will *trade up* to *m* (she will leave her current match and instead match with
*m*).  The only way for this match to be broken is for a higher ranking man to
propose to *w*, but *m* is *w*'s top choice so they will be matched in any
stable pairing.

Also consider the instability side.  Assume a stable pairing of *w* to some
other man *m'*.  The second type of instability assumes there is no man *m* who
is ranked higher according to *w* AND prefers *w* to their current match.  Given
that *m* and *w* are each others top choice any final matching of *w* to NOT *m*
would result in an instability.

```
(b) If w is the last choice of m, and m is the last choice of w, then m and w 
    must be paired with each other in any stable matching.
```
My answer is this is false.  While *m* and *w* MAY be paired with each other in
a stable matching, they can (and likely would) each be paired with someone else.

Consider:
```
m1 w1 w2
m2 w1 w2

w1 m2 m1
w2 m1 m2
```

Given a male's propose algorithm, the steps would be:
```
m1 propose to w1 (provisionally accepted)
m2 propose to w1 (w1 gives m1 the boot and accepts m2)
m1 propose to w2 (provisionally accepted)
end (all parties are engaged)
```

There is no instability in the pairings of m1-w2 and m2-w1 proving (b) false.

###### 2) Dijsktra's shortest path algorithm
Dijsktra's algorithm requires all edge weights to be non-negative.  Show by
constructing an example that the algorithm can fail to compute the shortest path
between source and target when the graph contains a negative edge.






[1]:https://en.wikipedia.org/wiki/Stable_marriage_problem

