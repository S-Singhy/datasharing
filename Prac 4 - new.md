<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"> </script>

# FIT9059 Week 4: Practical Session 

This practical session is concerned with Complexity and Sorting by Divide-and-Conquer.

Like every week, it is unlikely that you will be able to complete all exercises during the prac session. If you don't and provided you find the time in your review schedule, I recommend you try to complete them at home.  On the other hand, if you finish all tasks before the prac ends, please try to tackle those tasks that you did not complete in the previous prac session. 

**Note**: As every week this session is assessed for active participation. The two questions used for this purpose are marked below. The Practical Sheet for Week 2 outlined  how to demonstrate active participation. This also applies to the present session.


Remember, your tutors are here to help you.

_Enjoy!_

1. **Complexity of the Celebrity Problem**

    Last week we discussed the celebrity problem. In the practical session  you derived its runtime complexity informally. We used the number of questions asked as a proxy for runtime.  If you need a refresher, please have another look at last week's prac sheet. This week you are asked to derive the same result formally by writing down the runtime recurrence relation for the runtime $T(n)$ and by solving this equation using backward substitution (also called telescoping). As before we will measure runtime simply as the number of questions asked.
<br>

1. **Complexity of Towers of Hanoi**

    We have discussed the _Towers of Hanoi_ puzzle during the lecture. Recall its recursive solution. The (somewhat simpler) solution we used in the lecture is
    
        Algorithm hanoiA(n, A, B, C)
            input: the number n of disks to move;
                   the peg identifier for the start and destination peg
                   a fixed intermediate (empty) peg C
            
            (* to move n disks from A to B *)
            (* recursively move (n-1) disks from A to C *)
            hanoiA(n-1, A, C)
            move the remaining largest disk from A to B
            (* recursively move (n-1) disks from C to A *)
            hanoiA(n-1, C, A)
            (* now we have the same state as at the start but for n-1 disks *)
            (* recursively move (n-1) disks from A to B *)
            hanoiA(n-1, A, B)
            
    We can handle this somewhat shorter and more efficiently by not moving the disks back to the starting peg but instead reassigning the roles of the pegs:
    
        Algorithm hanoiB(n, A, B, C)
            input: the number n of disks to move;
                three peg identifiers 
            (* to move n disks from A to B using the empty intermediate peg C *)
            (* recursively move (n-1) disks from A to C *)
            hanoiB(n-1, A, C, B)
            move the remaining largest disk from A to B
            (* recursively move (n-1) disks from C to B via the now empty peg A *)
            hanoiB(n-1, C, B, A)
                
    We are now interested in the runtime complexity of this solution. Define a recurrence relation for the runtime $T(n)$ in dependence on the number of disks. What is the measure of problem size? What can you use as the proxy for runtime? Note that there are two or three recursive calls in HanoiA and HanoiB, respectively! Write down and try to solve recurrence relations for both. You cannot solve these by using the Master Theorem. Why? Solve them by telescoping. 

    **Discuss your solution with your tutor.**
<br>

1. **Space requirements of list functions**

    The list functions that you have implemented before perform a significant amount of copying, for example, when _rest_ is used. Determine how much additional space the algorithms require to store intermediate parameters on the recursive call stack. Before doing so, you may want to revise the recurrence relations and the notes about array parameter passing in Python (which works essentially in the same way as these functions). Start by analysing how much space the functions _length_ and _find_ require. 

    **Discuss your reasoning with your tutor.**
<br>

1. **Functional Mergesort**
    Extend your list ADT class from the previous exercise with a function for mergesort as discussed in the lecture. The function should be a new method in this class (or in a subclass).
<br>


1. **Stability of Sorting Algorithms** (optional)

    Which of the sorting algorithms that you have studied are stable, which are not? Does this depend on any particular conditions of the implementation?
<br>

1. **Almost in-situ Mergesort** (optional)

    Your task  is to write a mergesort that runs _in-situ_. For this task, you should not start from the implementation you built on top of the list ADT class, but from the array-based implementation given in the online book. An attempt to perform in-situ mergesort in Python must start with removing the slicing operations from the function and instead passing index positions as parameters that identify the start and the end of the relevant part of the array, much like we did in the implementation of quicksort. In mergesort we call this "relevant part" a run. 
    
    Assume that you have an Array A with _n_ elements. If you have one sorted run from A[0] to A[n/2] and sorted run from A[n/2+1] to A[n-1], the merge operation should generate a single sorted run from A[0] to A[n-1] from these. 
    
    While it was quite easy to do the pivot-based selection in quicksort fully in place, it turns out that merging an array fully in place is everything but easy.
    
    However, if you employ a second array of the same size B[0...n-1] it becomes quite straight forward. The way to do so is to merge the two runs of A into B first, and then to copy the contents of B back into A. Since B can be reused for every merge, this only requires O(n) additional space in total. Whether one calls this _in-situ_ or not is a matter of taste, but it is not too bad in practice.
    
    Implement an almost _in-situ_ Mergesort based on this approach.
<br>
    
1. **Empirical performance evaluation** (optional)

    Conduct an empirical perfromance evaluation and comparison for your almost _in-situ_ Mergesort and for the functional Mergesort implementation you constructed in the beginning of this week's prac. In other words, gather actual runtime data for a relevant range of problem sizes and draw a plot of the runtimes in dependence on problem size. To do this, you can use the Python Library **timeit** (Recall that we used this in the lecture to time the runtime examples at the beginning of the first lecture about O-Notation). At which conclusions do you arrive? 
   
    You can find the full documentation for how to use in the offical Python docs: [https://docs.python.org/2/library/timeit.html](https://docs.python.org/2/library/timeit.html).
<br>



<!--
1. **Recursive List Handling**
    In the last practical session you defined an ADT class for lists based on recursive list definitions. (You may want to use last week's prac sheet to revise). If you did not complete this, you can ask your tutor for a master solution. Extend this class with two new functions *zip*, and *merge*. 

    | **Operator** | **Input**         | **Output** | **Description**                                   |
    |--------------|-------------------|------------|---------------------------------------------------|
    | _zip_          | Lists x, y    | List       | constructs a new list that contains the elements of x and y in alternating order |
    |              |                   |            | for example, zip([1,7,9],[5,4,3])=[1,5,7,4,9,3]   |
    | _merge_        | Lists x,  y    | List       | merges two sorted lists x and y into a single sorted list|
    
    **Discuss your solution with your tutor.**
<br>
-->