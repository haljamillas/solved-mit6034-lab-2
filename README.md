Download Link: https://assignmentchef.com/product/solved-mit6_034-lab-2
<br>
To work on this problem set, you will need to get the code, much like you did for the first two problem sets.

Your answers for the problem set belong in the main file lab2.py.

<strong>Search  </strong>

<h1>Explanation</h1>

This section is an explanation of the system you’ll be working with. There aren’t any problems to solve. Read it carefully anyway.

This problem set will involve implementing several search techniques. For each type of search function you are asked to write, you will get a graph (with a list of nodes and a list of edges and a heuristic), a start node, and a goal node.

A graph is an object of type Graph, defined in search.py, that has lists .nodes and .edges and a dictionary .heuristic (you won’t need to access the dictionary directly). All the graphs used by the tester are defined in graphs.py.

A node is just a string representing the name of the node.

An Edge is an object with attributes .name (a string), .node1 (a string, the node at one end of the edge), .node2 (a string, the node at the other end of the edge), and .length (a number).




You will need the following methods:

<ul>

 <li>get_connected_nodes(node): Given a node name, return a list of all node names that are connected to the specified node directly by an edge.</li>

 <li>get_edge(node1, node2): Given two node names, return the edge that connects those nodes, or None if there is no such edge.</li>

 <li>get_heuristic(start, goal): Given the name of a starting node in the graph and the name of a goal node, return the heuristic value from that start to that goal. If that heuristic value wasn’t supplied when creating the graph, then return 0.</li>

</ul>

You might also want to use the following methods:

<ul>

 <li>are_connected(node1, node2): Return True iff there is an edge running directly between node1 and node2; False otherwise.</li>

 <li>is_valid_path(path): Given ‘path’ as an ordered list of node names, return True iff there is an edge between every two adjacent nodes in the list, False otherwise.</li>

</ul>

In addition, you’re expected to know how to access elements in lists and dictionaries at this point. For some portions of this lab, you may want to use lists like either stacks or queues, as documented at &lt;<a href="https://docs.python.org/tut/node7.html">http://docs.python.org/tut/node7.html</a><a href="https://docs.python.org/tut/node7.html">&gt;</a>. However, you should NOT import other modules (such as deque), because it will confuse the tester.

You also may need to sort Python lists. Python has built-in sorting functionality, documented at &lt;<a href="https://wiki.python.org/moin/HowTo/Sorting">http://wiki.python.org/moin/HowTo/Sorting</a><a href="https://wiki.python.org/moin/HowTo/Sorting">&gt;</a>.

<h1>The Agenda</h1>

Different search techniques explore nodes in different orders, and we will keep track of the nodes remaining to explore in a list we will call the <strong>agenda</strong> (in class we called this the <strong>queue</strong>). Some techniques will add paths to the top of the agenda, treating it like a stack, while others will add to the back of the agenda, treating it like a queue. Some agendas are organized by heuristic value, others are ordered by path distance, and others by depth in the search tree. Your job will be to show your knowledge of search techniques by implementing different types of search and making slight modifications to how the agenda is accessed and updated.

<h1>Extending a path in the agenda</h1>

In this problem set, a path consists of a list of node names. When it comes time to extend a new path, a path is selected from the agenda. The last node in the path is identified as the node to be extended. The nodes that connect to the extended node, the adjacent nodes, are the possible extensions to the path. Of the possible extensions, the following nodes are NOT added:

<ul>

 <li>nodes that already appear in the path.</li>

 <li>nodes that have already been extended (if an extended-nodes set is being used.)</li>

</ul>

As an example, if node <em>A</em> is connected to nodes <em>S</em>, <em>B</em>, and <em>C</em>, then the path [‘S’, ‘A’] is extended to the new paths [‘S’, ‘A’, ‘B’] and [‘S’, ‘A’, ‘C’] (but not [‘S’, ‘A’, ‘S’]).

The paths you create should be new objects. If you try to extend a path by <em>modifying</em> (or “mutating”) the existing path, for example by using list .append(), you will probably find yourself in a world of hurt.

<h1>The Extended-Nodes Set</h1>

An extended-set, sometimes called an “extended list” or “visited set” or “closed list”, consists of nodes that have been extended, and lets the algorithm avoid extending the same node multiple times, sometimes significantly speeding up search. You will be implementing types of search that use extended-sets. Note that an extended-nodes set is a set, so if, e.g., you’re using a list to represent it, then be careful that a maximum of one of each node name should appear in it. Python offers other options for representing sets, which may help you avoid this issue. The main point is to check that nodes are not in the set before you extend them, and to put nodes into the extended-set when you do choose to extend them.

<h1>Returning a Search Result</h1>

A search result is a path which should consist of a list of node names, ordered from the start node, following existing edges, to the goal node. If no path is found, the search should return an empty list, [].

<h1>Exiting the search</h1>

Non-optimal searches such as DFS, BFS, Hill-Climbing and Beam <strong>may</strong> exit either:

<ul>

 <li>when it finds a path-to-goal in the agenda</li>

 <li>when a path-to-goal is first removed from the agenda.</li>

</ul>

Optimal searches such as branch and bound and A* <strong>must</strong> always exit:

<ul>

 <li>When a path-to-goal is first removed from the agenda.</li>

</ul>

(This is because the agenda is ordered by path length (or heuristic path length), so a path-to-goal is not necessarily the best when it is added to the agenda, but when it is removed, it is guaranteed to have the shortest path length (or heuristic path length).)

For the sake of consistency, you should implement all your searches to exit:

<ul>

 <li><strong>When a path-to-goal is first removed from the agenda.</strong></li>

</ul>

<h1>Multiple choice</h1>

This section contains the first graded questions for the problem set. The questions are located in lab2.py and let you check your knowledge of different types of search. You should, of course, try to answer them before checking the answers in the tester.

<h1>Optional Warm-up: Breadth-first Search and Depth-first Search</h1>

This section is optional. You should do it if you want to get a better understanding of the basics of search.

The first two types of search to implement are breadth-first search and depth-first search. You should <strong>allow backtracking</strong> for the search.

Your task is to implement the following functions:

def bfs(graph, start, goal):

def dfs(graph, start, goal):

The inputs to the functions are:

<ul>

 <li>graph: The graph</li>

 <li>start: The name of the node that you want to start traversing from</li>

 <li>goal: The name of the node that you want to reach</li>

</ul>

When a path to the goal node has been found, return the result as explained in the section <strong>Returning a Search Result</strong> (above).

<strong>Using Heuristics  </strong>

<h1>Hill Climbing</h1>

Hill climbing is very similar to depth first search. There is only a slight modification to the ordering of paths that are added to the agenda. For this part, implement the following function:

def hill_climbing(graph, start, goal):

The hill-climbing procedure you define here <em>should</em> use backtracking, for consistency with the other methods, even though hill-climbing typically is not implemented with backtracking. Hill-climbing does not use an extended-set.

For an explanation of hill-climbing, refer to <a href="http://courses.csail.mit.edu/6.034f/ai3/ch4.pdf">Chapter 4</a> of the textbook (page 8 of the pdf, page 70 of the textbook).

<h1>Beam Search</h1>

Beam search is very similar to breadth first search, but there is a modification to what paths are in the agenda. The agenda at any time can have up to <strong>k</strong> paths of each length <strong>n</strong>; <strong>k</strong> is also known as the <strong>beam width</strong>, and <strong>n</strong> corresponds to the level of the search graph. You will need to sort your paths by the graph heuristic to ensure that only the best <strong>k</strong> paths at each level are in your agenda. You may want to use an array or dictionary to keep track of paths of different lengths. Beam search does NOT use an extendedset, and does NOT use backtracking to the paths that are eliminated at each level.

Remember that <strong>k</strong> is the number of paths to keep at an <em>entire level</em>, not the number of paths to keep from each extended node.

Also remember that beam search sorts paths by <em>just</em> the heuristic value, not the path length (as branchand-bound does) or the path length + heuristic value (as A* does).

For this part, implement the following function:

def beam_search(graph, start, goal, beam_size):

For an explanation and an example of beam search, refer to <a href="http://courses.csail.mit.edu/6.034f/ai3/ch4.pdf">Chapter 4</a> of the textbook (pages 13-14 of the pdf). However, this example is incorrect according to the way we do beam search: at the third level, the node B (with heuristic value 6.7) should not be included, only C and F should be included (since the beam width is 2), so at the fourth level, B should not be extended to A and C.

<h1>Optimal Search</h1>

The search techniques you have implemented so far have not taken into account the edge distances. Instead we were just trying to find one possible solution of many. This part of the problem set involves finding the path with the shortest distance from the start node to the goal node. The search types that guarantee optimal solutions are branch and bound and A*.

Since this type of problem requires knowledge of the length of a path, implement the following function that computes the length of a path:

def path_length(graph, node_names):

The function takes in a graph and a list of node names that make up a path in that graph, and it computes the length of that path, according to the “LENGTH” values for each relevant edge. You can assume the path is valid (there are edges between each node in the graph), so you do not need to test to make sure there is actually an edge between consecutive nodes in the path. If there is only one node in the path, your function should return 0.

<h1>Branch and Bound</h1>

Now that you have a way to measure path distance, this part should be easy to complete. You might find the list procedure remove, and/or the Python ‘del’ keyword, useful (though not necessary). For this part, complete the following:

def branch_and_bound(graph, start, goal):

Branch-and-bound does not use an extended-set.

For an explanation of branch-and-bound, refer to <a href="http://courses.csail.mit.edu/6.034f/ai3/ch5.pdf">Chapter 5</a> of the textbook (page 3 of the pdf).

<h1>A*</h1>

You’re almost there! You’ve used heuristic estimates to speed up search and edge lengths to compute optimal paths. Let’s combine the two ideas now to get the A* search method. In A*, the path with the least (heuristic estimate + path length) is taken from the agenda to extend. A* always uses an extendedset — make sure to use one. (Note: If the heuristic is not consistent, then using an extended-set can sometimes prevent A* from finding an optimal solution.)

def a_star(graph, start, goal):

<h1>Graph Heuristics</h1>

A heuristic value gives an approximation from a node to a goal. You’ve learned that in order for the heuristic to be admissible, the heuristic value for every node in a graph must be less than or equal to the distance of the shortest path from the goal to that node. In order for a heuristic to be consistent, for each edge in the graph, the edge length must be greater than or equal to the absolute value of the difference between the two heuristic values of its nodes.

In lecture and tutorials, you’ve seen examples of graphs that have admissible heuristics that were not consistent. Have you seen graphs with consistent heuristics that were not admissible? Why is this so?

For this part, complete the following functions, which return True iff the heuristics for the given goal are admissible or consistent, respectively, and False otherwise:

def is_admissible(graph, goal):

def is_consistent(graph, goal):

<h1>Survey</h1>

Please answer these questions at the bottom of your lab2.py file:

<ul>

 <li>How many hours did this problem set take?</li>

 <li>Which parts of this problem set, if any, did you find interesting?</li>

 <li>Which parts of this problem set, if any, did you find boring or tedious?</li>

</ul>

<h1>Common Complaints</h1>

Complaint: All of the search functions we have to implement are so similar.

Response: They’re similar, but you should understand in detail how each one works. If you want, you can try implementing a single search function (like the flow-chart shown in lecture), and then implementing each of the individual searches as a call to this function with different parameters.

Complaint: Most of these searches are non-optimal and not even used in practice.

Response: The goal is to teach you the theory behind search, not just the best way to do it.

Complaint: This lab is tedious to debug.

Response: That’s the case with most things. Make sure to read the problem description thoroughly, and remember that the TAs are there to help.

<h1>FAQs</h1>

Q: For SAQG, my implementation of depth-first search finds the path SG, but the tester only accepts SAG and SQG.

A: This is based on some assumptions about the order in which you’re traversing the search tree. If you use the graph.get_connected_nodes function, you’ll end up getting them in the right order.

Q: For AGRAPH, my implementation of A* finds the path SBACG (which has a length of 13), but the tester says it should be SACG (which has a length of 14). Isn’t A* always supposed to find the shortest path?

A: Not necessarily. Make sure you’re using your extended-list correctly.







MIT OpenCourseWare <a href="http://ocw.mit.edu/">http://ocw.mit.edu</a>

6.034 Artificial Intelligence

Fall 2010

For information about citing these materials or our Terms of Use, visit: <a href="http://ocw.mit.edu/terms">http://ocw.mit.edu/terms</a><a href="http://ocw.mit.edu/terms">.</a>