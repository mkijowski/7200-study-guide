### Using this quide
No idea, gonna be scattered until I get a better handle on it.
Maybe expect it to become pdf for latex engine to allow better equestions?

Exam:
* stable marriage, matching, perfect mathcing, derive stable solution
* complexity, big 0 notation, in line with sample problem given a number of
  functions
* algorithm design, variant of something we've already seen (greedy algorithm)
* algorithm design / pseudo code similar to assignment
  * sort, walk thorugh, collect or not collect
* greedy algorithm
* maybe little bit on divide and conquer
* covers up until last class (Tuesday, Oct. 8)

Things I think T.K. wants us to know:

* Know trees, binary, three-ary, be able to figure out depth of trees
* recursive tree application to a problem that doesnt allow for master theorem


### Deriving Master Theorem (and possibly Muster)
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

### Sorting
quick sort, bubble sort, merge sort, etc
describe that many of the algorithms apply sorting as a pre-requisite to the
algorithm

