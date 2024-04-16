20240309 - 15:43

Status: #idea

Tags:

# Midterm Recap
## Lecture 1
Programs can be seen as data which can be processed by other programs. 

Introduction to T-diagrams. 
![[Pasted image 20240309155109.png]]
This is an x86-64 processor. 

![[Pasted image 20240309155225.png]]
This is a program "Tetris" written in x86-64 code. 

![[Pasted image 20240309155257.png]]
And this is the program "Tetris" running on x86-64 processor.

> [!info]
> Interpreter is a program that executes another program. Interpreter's source language is the language in which the interpreter is written. The interpreter's target language is the language in which the programs are written, which the interpreter can execute. 

![[Pasted image 20240309155932.png]]
T-diagram for an interpreter. Chrome browser for PC, seen as interpreter for Javascript. 

We can stack these on each other to create following: 
![[Pasted image 20240309160058.png]]
This is a browser which acts as an interpreter for Javascript. 

>[!note]
> Compiler is a program that translates other programs from one language to another. The language of the programs we give to the compiler are called the from-language. The language of the programs we get back from the compiler is called the to-language. 

![[Pasted image 20240309160305.png]]
The compiler looks like a T in the T-diagram. Here we are compiling "SA editor" from Typescript to JavaScript. 

Fundamental ideas from this is that compilers and interpreters are just programs. 

![[Pasted image 20240309161751.png]] Small-step semantics: Keep applying contractions until we arrive at a result. The contraction is based on the contraction relation. In each step we apply contraction wherever possible. 

![[Pasted image 20240309162120.png]]
Static type check is about trying to find when statements don't make any sense. We know what result we can expect based on the input and operator. 

Denotational semantics: Introduce a semantic function that directly assigns a result value to a program.  

Look at virtual machines. 

## Lecture 2
This lecture will look at recursive interpreters. 

Introduce a semantic function that directly assigns a result value to a program. ![[Pasted image 20240312154428.png]]

We then add rules to the semantic function which are inline with the expected behavior. 
![[Pasted image 20240312154602.png]]

The final action done in a program will be what is returned.

To denote environment $\Delta$. Using the environment we can make use of variables. 
![[Pasted image 20240312155005.png]]

Semantic function for a program execution uses ![[Pasted image 20240312155302.png]]. With this knowledge we can now express things such as: 
![[Pasted image 20240312155331.png]]
This looks quite confusing to lets break it down, if we run x=3 in the empty environment the program execution will return 3, the environment will be the empty one appended with a mapping between x and 3.

As we want to have more than just a single environment we will use recursive environments.

W e will have a evaluate function which handles different program types in different ways. When we reach a block we will find the body, locals and unassigned values, then recursively run the evaluate function again on this block. 

Another issue is how we differentiate between return values and our function not returning anything, we can once again add a new part to our evaluate function. 

The issue with this approach is that we have a lot of overhead with our interpreter. 

Main takeaways: We have 2 new symbols, one is for evaluating a expression and the other for evaluating an entire function. We then use recursion to break our program into runnable parts. This has a lot of overhead.

## Lecture 3
We now move on to the explicit-control-evaluators

Here we introduce the concept of a control stack and a stash. We will then expand the expression on the control and place values on the stash which we need for later. When we are done with evaluating our program we can find the result on the top of the stash. 

We will then expand this idea so we can use conditionals, Booleans and sequences. 

Sequences are solved by splitting the sequence into components, and then we add a pop after each of the sequence parts.
![[Pasted image 20240312194226.png]]

When we reach a block we will extend current environment by frame with declared names. Then set current environment to start at new frame, pop block from control and push body of block on control.

We deal with lambda expression by creating function value, function value gets current environment, push reference to function value on stash. 

To restore previous environments we have a "restore environment" instruction. 

Now we move on to transitive function. 
![[Pasted image 20240313090603.png]]

We than apply this to all our known operations:
![[Pasted image 20240313090705.png]]


## Lecture 4
Now an idealized virtual machine. 

New machine language S0VML.
![[Pasted image 20240313090940.png]]

Transitive function ![[Pasted image 20240313091014.png]]

![[Pasted image 20240313091101.png]]

We than use a program counter to keep track of the current instruction we're on. Also a operand stack. 

![[Pasted image 20240313091324.png]]

We implement this by going through each part of the program and translating it into machine code, and finally adding a done instruction.

After this we run the code by going through each of these micro instructions. 

## Lecture 5
We now move on to a more realistic VM. Up to this point we are still making heavy use of JavaScript's data structures. 

We are currently linearly searching through chain of frames, we can improve this by implementing lexical addressing where the connection between variables and their declaration is static, so we can predict in what frame and exactly where any variable can be found. 

We can also use heap allocation to better store values. We can either do this using pointer tagging, where we add type information to pointers. Alternatively use NaN boxing where we use the "free" NaN bits to store information.

Finally we discussed string pooling. Which allow us to dynamically integrate created string into memory management.

## Lecture 6
We looked at 3 different memory allocation types. 

Static allocation assigns a fixed memory location to each identifier, the downsides are that the size of each data structure must be known at compile-time, recursive functions are not possible and data structures such as closures can't be created dynamically. 

Stack allocation, keep track of information on function invocations on runtime stack. We can now use recursive and size of locals can depend on arguments. But it's difficult to manipulate recursive data structures, and only objects with known compile time size can be returned from functions.

Heap allocation, data structures can now be allocated or deallocated in any order, complex pointer structures will evolve at runtime. But now management of allocated memory becomes an issue.

In the heap memory model we can think of the memory as a graph. We have nodes which are stack frames, operand stack, environments etc. The edges refer to references between nodes. We have labels on edges. Nodes can point to primitive values. 

We then get a ton of rules. 

There are a few different ways of managing the heap size. 

The first is reference counting where we simply keep track of how many references each node has to it. If it reaches zero we can confidently delete the node. The advantages is that is incremental, has good locality and has immediate reuse. The big downside is that it can't reclaim cyclic data structures.

The next is mark-sweep garbage collection. We use a freelist but when we run out of space in our memory we try to reclaim nodes. We do this by starting at the root and seeing which nodes can be found. Mark all found as alive, all unmarked can be freed. See slides for performance. The disadvantages are fragmentation and poor locality. 

The final version is copying garbage collection. The idea is to only use half of the available nodes. Once this half is filled, copy the live memory contained in the first half to the second, only moving alive nodes.

![[Pasted image 20240313093900.png]]jjj


\-\-\-
# References