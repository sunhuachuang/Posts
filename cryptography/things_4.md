### [复杂度类P](https://bristolcrypto.blogspot.com/2014/10/52-things-number-4-complexity-class-p.html)

```
The Complexity Class P
复杂度类P
```

Most of the content of this post is a reworking of parts of Introduction to the Theory of Computation by Michael Sipser [1], which I have found hugely helpful.

Section 1: Complexity and Big O Notation

We want to know how difficult a given task is for a computer to do in order to design efficient programs. The trouble is that the processing power of a computer varies massively depending on the hardware (e.g. see last week's '52 Things' blog). So we want a measure of the difficulty of a task that doesn't depend on the specific details of the machine performing the task. One way to do this is to bound the number of operations that a certain model of a computer would take to do it. This is called (time) complexity theory.

Typically, though, the number of operations required will depend on the input to the task and may vary even with inputs of the same length. As a pertinent example, say we design a computer program which tells you whether or not an integer you input is prime. If we give as input the number 256, the program will probably output 'not prime' sooner than if we had given it the number 323 (even though they both have length 9 when written as binary integers, for example), since the first integer has a very small prime factor (2) and the second has larger factors (17 and 19). Therefore we usually opt for a worst-case analysis where we record the longest running time of all inputs of a particular length. So we obtain an algebraic expression t(n) that reflects the longest running time of all inputs of length n.

Furthermore, when the input length n becomes very large, we can neglect all but the most dominant term in the expression and also ignore any constant factors. This is called asymptotic analysis; we assume n is enormous and ask roughly how many steps the model of computation will take to 'finish' when given the worst possible input of length n, writing our answer in the form O(t(n)). For example, if we find that our process takes 6n3–n2+1 steps, we write that it is O(n3), since all other terms can be ignored for very large n.

Section 2: Turing Machines

Now we give the model that is most often used in the kind of calculations performed in Section 1. First, recall that an alphabet is a non-empty finite set and a string is a finite sequence of elements (symbols) from an alphabet. A language is simply a set of strings.

A Turing machine models what real computers can do. Its 'memory' is an infinitely long tape. At any time, each square of the tape is either blank or contains a symbol from some specified alphabet. The machine has a tape head that can move left or right along the tape, one square at a time, and read from and write to that square. At first, the tape is all blank except for the leftmost n squares which constitute the input (none of which can be blank so that it is clear where the input ends). The tape head starts at the leftmost square, reads the first input symbol and then decides what to do next according to a transition function. The transition function depends on what it reads at the square it is currently on and the state that the machine is currently in (like a record of what it has done so far) and returns

    a new state
    another symbol to write to the square it is on (though this symbol might be the same as what was already written there)
    a direction to move in: left or right.

The machine will continue to move one square at a time, read a symbol, evaluate the transition function, write a symbol and move again, until its state becomes some specified accept state or reject state.

If the machine ends up in the accept state, we say it accepts its input. Similarly it may reject its input. In either case we say the machine halts on its input. But note that it may enter a loop without accepting or rejecting i.e. it may never halt. If a Turing machine accepts every string in some language and rejects all other strings, then we say the machine decides that language. We can think of this as the machine testing whether or not the input string is a member of the language. Given a language, if there is a Turing machine that decides it, we say the language is decidable.

The power of this model comes from the fact that a Turing machine can do everything that a real computer can do (this is called the Church-Turing thesis [2]). We define the time complexity class TIME(t(n)) to be the collection of all languages that are decidable by an O(t(n)) time Turing machine, then we turn computational problems into questions about language membership (is an input string a member of a certain language? e.g. does this string representing an integer belong to the language of strings representing prime integers?) and can partition computational problems into time complexity classes.

Section 3: The Complexity Class P

Finally, we arrive at the purpose of this blog! If t(n)=nk for some k>0 then O(t(n)) is called polynomial time. The complexity class P is the class of all languages that are decidable in polynomial time by a Turing machine. Since k could be very large, such Turing machines are not necessarily all practical, (let alone 'fast'!), but this class is a rough model for what can be realistically achieved by a computer. Note that the class P is fundamentally different to those languages where t(n) has n in an exponent, such as 2n, which grow much, much faster as n increases – so fast that even if you have a decider for some language, you may find that the universe ends before it halts on your input!

We conclude with an example of a polynomial time problem. Suppose you have a directed graph (a set of nodes and edges where there is at most one edge between any pair of nodes and each edge has an arrow indicating a direction). Then if we encode the graph and the two nodes as a single string, we can form a language consisting of those strings representing a graph and two nodes such that it is possible to follow the edges from the first node and eventually arrive at the second. So a decider for this language will effectively answer the question of whether there is a path from the first node A to the second B, called the path problem, by accepting or rejecting the graph and nodes you input. We give a decider for this language and show that it decides in polynomial time.

    First put a mark on A.
    Scan all the edges of the graph. If you find an edge from a marked node to an unmarked node, mark the unmarked node.
    Repeat the above until you mark no new nodes.
    If B is marked, accept. Otherwise, reject.

This process successively marks the nodes that are reachable from A by a path of length 1, then a path of length 2, and so on. So it is clear that a Turing machine implementing the above is a decider for our language. Now we consider the time complexity of this algorithm. If we couldn't do steps 1 and 4 in polynomial time, our machine would be terrible! So we focus on steps 2 and 3. Step 2 involves searching the input and placing a mark on one square, which is clearly polynomial time in the size of the input. Step 3 repeats step 2 no more times than the number of nodes, which is necessarily less than the size of the input (since the input must encode all the nodes of the graph) and is hence polynomial (in particular, linear) in the size of the input. Therefore the whole algorithm is polynomial time and so we say the path problem is in P.

[1] http://www.amazon.co.uk/Introduction-Theory-Computation-Michael-Sipser/dp/0619217642
[2] http://en.wikipedia.org/wiki/Church%E2%80%93Turing_thesis
