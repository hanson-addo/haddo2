## Details
* Motivation
The Travelling Salesman Problem is a classic NP-Hard problem: find the minimum cost path that visits every node in a graph. Even in it’s “decision problem” form it is NP-Complete (“is there a path that visits every node with at most cost k”). The simplest brute force solution to the problem tries every valid permutation of vertices to visit and sums up the cost (for a runtime of approximately n!). A number of improvements exist that reduce it down near-ish to O(2n), but that is still an intractable problem.
We’re going to work on a Euclidean TSP problem where (1) the “vertices” in the graph represent cities with a physical location in the world, and therefore (2) they satisfy the triangle inequality (it is faster or equally as fast to go directly to your destination, than to go somewhere else and then to your destination). This is a very common variation of the problem which is still hard, but has a simple approximation algorithm that we can implement with the tools we’ve discussed in CS483: use Prim’s Minimum Spanning Tree algorithm to get a MST, perform a Depth First Traversal of that tree and visit the cities in the order you encounter them (making it a pre-order DFT).
In this project you’re going to implement both the simple brute force try-every-possibility algorithm (we’ll call this TSP-Permutation) as well as the approximation algorithm (we’ll call this TSP-Approx) in a larger framework that will allow you to visualize the algorithm steps. I’m providing some guidance in this document, but there are very specific instructions in the code base to allow you to complete this project.
The Simulator
This project has a large code base where you will be inserting your contribution. The majority of this code is there to provide you with a visual display of your work once you are done. As it is, the code base can be compiled and run with the following commands from your user directory on Windows:
       javac -cp .;483libs.jar *.java
       java -cp .;483libs.jar SimGUI
Or the following commands on MacOS/Linux:
       javac -cp .:483libs.jar *.java
       java -cp .:483libs.jar SimGUI


A randomly generated graph will be displayed twice (once for each algorithm), with random city names and edge distances appropriate to the location where they were first created (as shown). You can click and drag cities around for better viewing, but this does not alter the distances.
There is a “step” button and “play” button which will play the algorithms (but only after you write them!). The “reset” button should work out-of-the-box, it will just give you a new random graph of the same type.
The following three commands will also work to run the simulator with more parameters:
java -cp .;483libs.jar SimGUI [number-of-cities]
java -cp .;483libs.jar SimGUI [number-of-cities] [rng-seed]
java -cp .;483libs.jar SimGUI [number-of-cities] [rng-seed] [ms-delay]
[number-of-cities] can be between 2 and 10, [rng-seed] can be any integer value, and [ms-delay] controls the simulation drawing-delay (minimum 1ms). For example, if you want 6 cities, generated with a random number generator seeded with 1034, and a 1ms delay for drawing, you’d use:
       java -cp .;483libs.jar SimGUI 6 1034 1
Calling with no parameters gives defaults of 5, 0, and 100 to the above parameters respectively.

** The JUNG Library and Provided Code Base
* The JUNG library (Java Universal Network/Graph Framework, http://jung.sourceforge.net) provides a lot of cool visualization tools for graphs, such as automatic layouts, an easy interface for creating/editing graphs, and much more. The remainder of the code base (except PermutationIterator) was written by us utilizing the JUNG library heavily. PermutationIterator has a header with information on its origin and licensing information for those interested.
Below is an overview of the code base provided:
• SimGUI – The simulator itself.
• GraphNode – a general-purpose graph node class for the simulator
• City – extends graph node class for city-specific things (like city names)
• GraphEdge – a general-purpose graph edge class for the simulator
• Flight – extends graph node class for flight-specific things
• FourEightyThreeAlg – an interface for all CS483 algorithms for use in the simulator
• TSPAlg – an abstract class with a lot of helper code for TSP algorithms (esp. displaying them)
• TSPPermutation – code to display the TSP-by-permutation an algorithm step-by-step
• PermuationIterator – a helper class for TSPPermutation
• TSPApprox – code to display the TSP-by-approximation an algorithm step-by-step
>>>>>>> de6f7e9 (first commit)
