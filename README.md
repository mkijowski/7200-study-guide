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

Will likely be a greedy algorithm.  Greedy algorithm always stays ahead.  Show
that after each step of the greedy algorithm, its solution is at least as good
as any other algorithm.

#### Interval scheduling
Greedy algorithm, consider jobs in increasing order of finish time:
```
Sort jobs by finish times so that f1 <= f2 <= ... <= fn.
A <- empty 
for j = 1 to n {
   if(job j compatible with A)
   A <- A U {j}
}
return A
```
runs in O(n log n)

#### Interval partitioning
Consider lectures in increasing order of start time: assigning lectures to any compatible classroom
```
Sort intervals by starting time so that s1 <= s2 <= ... <= sn.
d <- 0  (number of allocated classrooms)

for j = 1 to n {
   if(lecture j is compatible with some classroom k)
      schedule lecture j in the classroom  kbest with lowest finish time
   else
      allocate a new classroom d + 1
      schedule lecture j in classroom d + 1
      d <- d + 1
}   
```
runs in O(n log n)

#### 
* algorithm design, variant of something we've already seen (greedy algorithm)
* algorithm design / pseudo code similar to assignment
  * sort, walk thorugh, collect or not collect

## Recursive tree and Master Theorem
#### Master Theorem
Let T(n) be a monotonically increasing function that satisfies 

`T(n) = a T(n/b) + f(n)` 

`T(1) = c`  

Where a >= 1, b >= 2, c>0.  If f(n) is O(n^d) where d >= 0 

then
```
       {  O(n^d)                        if a < b^d
T(n) = {  O( (n^d)(log n) )             if a = b^d
       {  O( n^(log<sub>b</sub> a ))    if a > b^d
```

* master theorem is comparing the effort between the recursive splitting step
  (divide and combine), and the solution effort of the simplest case.
* fourth condition to Master theorem is applied in the closest point algorithm
* its not that master theorem doesnt apply to non-polynomial functions, we just
  cant prove that it does apply

#### Muster Theorem
Subtract and conquer, let T(n) be a function defined on positive n having the
property:

`T(n) = a T(n-b) + f(n)`

`T(1) = c`

Where a > 0, b > 0, d >= 0, and f(n) is in O(n^d).

then
```
        {  O(n^d)              if a < 1
T(n) =  {  O(n^(d+1))          if a = 1
        {  O( (n^d)(a^(n/b)) ) if a > 1
```


##### Deriving Master Theorem (and possibly Muster)
* First, learn the recursion tree method. Learn how to build the tree, how to count the number of leaves, and how to count the amount of "extra work" at each level, and how to sum them (by summing a series, e.g., a geometric series).
* Next, open up a textbook read a standard proof of the Master theorem. Work through each step and check that you understand what's happening.
* Now, close your textbook and put away all your resources. Put a blank piece of paper in front of you... and derive the Master theorem yourself. How do you do that? Well, you use the recursion tree method. Try working through it by yourself and try to solve the recurrence entirely on your own. If you get stuck, as a last resort you can open the textbook back up and see how to proceed from there... but then the next day, you should try this exercise again.

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

Dihsktra's algorithm does not work on graph's with negative edge weights
because it assumes that once a node has been visited there will not be a
shorter path to that node.

Consider the following:
```
       A
      / \
     /   \
    5     2
   /       \
  /         \
  B--(-10)-->C
```

Finding the shortest distance from A to C, the algorithm will first visit A by
extracting it from `Q=[A,B,C]`. (note, distances are instantiated at `A=0,
B=infinity and C=infinity`.  
Updating the distances and Q we now have:

`Q=[B,C]   A=0    B=5   C=2`  

The algorithm will then extract `C` from `Q`.  Since C has no outgoing nodes the
distances remain the same and we get:

`Q=[B]     A=0    B=5   C=2`

Finally, the algorithm extracts `B` from `Q`.  Because of the constraint of 
positive numbers for vertex weights, the algorithm looks at outgoing edges
of vertex `B` going into any vertices in `Q`, but because `Q` is empty, the
algorithm does not consider that `A -> B -> C` could be shorter than `Q` so it
terminates with minimum distance from `A->C` being 2.

###### 3) Apply Kruskals algorithm to find the MST and it's weight
Kruskals algorithm starts without any edges and adds edges with the minimum cost
so long as they do not create a cycle.  If adding an edge would create a cycle
we simply do not add it and move on.  This would leave for this problem the
following MST:
```
L-S 263
L-P 388
L-N 168
S-D 630
D-H 243
P-B 561
```
For a weight of whatever the sum of the above numbers are...

###### 4) Consider the recurrence:
```
          T(3n/4) + T(n/5) + cn    if n >= 60
T(n) <=
          d                        if n <  60       
```
Give an expression/formula for the length of the shortest path from root to leaf
in the recursion tree.

The two lengths are log<sub>4/3</sub>*n* and log<sub>5</sub>*n* of which
log<sub>5</sub>*n* is shorter.

###### 5) Determine order-theoretic solutions to the following recurrences:

1. `T(n) = 5 T(n/7) + n`
   applying master theorm with `a = 5`, `b = 7`, and `d = 1` we get
   `5 < 7^1` therefor: `O(n)`
2. `T(n) = 2 T(n-1) + 1`
   applying muster theorem with `a = 2`, `b = 1`, and `d = 0` we get
   `a > 1` therefor: `O( (n^0)(2^(n/1)) ) == O(2^n)`

[1]:https://en.wikipedia.org/wiki/Stable_marriage_problem

