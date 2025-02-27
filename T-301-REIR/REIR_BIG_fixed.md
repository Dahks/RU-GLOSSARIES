
Scalability
- How efficient the program is as the input gets larger

Time complexity
- Time spent as a function of input size (or parameter) n


Order of growth
- Ignore leading coefficient
- What kind of function it is
	- constant
	- logarithmic
	- linear
	- linearithmic
	- quadratic
	- cubic
	- exponential

Predict performance
- measurements
	- run program for various input sizes and measure running time
	- doubling hypothesis
		- double size of input
		- b = lg(T(N) / T(N/2))
		- T(N) = a * N^b
- mathematical
	- To bound the order of growth, it suffices to focus on the most frequently executed statement (innermost loop f.x.)

2^10 ~ 10^3

Gagnatög
-


Euclid's algorithm
- Find prime factorization

2-sum
- Given n distinct integers, how many pairs sum to exactly zero

sum of integers from 0 to n = n(n+1) / 2

3-sum
- given n distinct integers, how many triples sum to exactly zero
	- (nC3) = N(N-1)(N-2)/3! = 1/6 N^3

Array access dominates running time'

Binary search
- given a sorted array  and a key, find index of the key in the array
	- start in middle
	- too small, go left
	- too big, go right
	- equal, found
- Invariant
	- if key appears in array a[], then a(lo) <= key <= a(hi)
- log(n)
- 1 + log(n) compares


Dynamic connectivity problem
- Given a set of N objects, support two operations
	- connect two objects
	- is there a path connecting the two objects

Union find
- init(n)
- union(int p, int q) - merge sets containing elements p and q
- find(int p)         - id for set containing element p
- implementations
	- quick-find (eager approach)
		- integer array id() of length n
		- id(p) identifies the set containing element p
			- union(p, q) -> change all p to q -> n
			- init() -> n
			- find() -> 1
		- processing a sequence of n union operations on n elements takes more than n^2 array accesses
	- Quick-union (lazy approach)
		- parent array of length i, parent(i) = parent of i in tree
		- find(p) - root of parent of p = log(n)
		- union(p,q) - set root of p to root of q + cost of finding two roots
			- teikna tré
	- weighted quick-union
		- avoid tall trees (always link root of smaller tree to root of larger tree)
		- extra array size() -> count of elements in tree rooted at i
		- add if statements to choose between root of p or root of q
			- init = n
			- union = log n + cost of finding two roots
			- log n

percolation
- top and bottom of n by n grid are connected by open sites


Stack -> LIFO (last in first out)
- resizing array (constant amortized)
- linked list (constant in worst case but extra time and space for links)

Queue -> FIFO (first in first out)

underflow -> already empty
overflow  -> full

Bag
- add
- size
- iterator (any order)

Stack, queue, bag
- insert
- remove 
- iterate
- is_empty()
- size

loitering: holding a reference to an object when it is no longer needed

resizing array --> array accesses are expensive
- if full -> array twice the size (1 amortized)
- if empty to quarter -> array half size (1 amortized)
- array is always between 25% and 100% full

Generic
- Allows you to implement any type

Autoboxing: automatic cast between a primitive type and its wrapper
syntactic sugar: behind-the-scenes casting
recursive function: function that calls itself (stack)

interface inheritance (subtyping)
- interface construct for declaring a relationship between otherwise unrelated clasess by specifying a common set of methods that each implementing class must nclude
- interfaces enable us to write client programs that can manipulate objects of varying types, by invoking common methods from the interface
	- comparable
	- iterable -> method that returns iterator


Iterator
- hasnext()
- next()


memory asdklfjalsdæjf 

empirical analyss
- execute program to perform experiments
- assume power law
- formulate a hypothesis for running time
- model enables us to make predictions

mathematical analysis
- analyze algorithm to count frequency of operations
- ues tilde notation to simplify analysis
- model enables us to explain behavior

scientific method
- mathematical model is independent of a particular system, applies to machines not yet built
- empirical analysis is necessary to validate mathematical models and to make predictions

total order
- any two items v,w, satisfy v < = or > w
- no cycle of < relationships


Selection sort
- fins smallest remaining entry and move to the current position
- swap a(i) and a(min) (scan from left to right)
- invariants: entries to the left of current in fixed and ascending order, above is in effectively random order, and every entry there is larger than an etnry to the left of current
- running time is insensitive to input
- data movement is minimal - linear number of exchanges (exactly n)
- quadratic time
- not stable

insertion sort
- scan from left to right, move current into correct position before current
- invariants
	- entries to the left of current, including current itself are in ascending order
	- entries to the right of current have not yet been seen
- 1/4 N^2 compares and exchanges on average
- for partially-sorted arrays, insertion sort runs in linear time
	- number of exchanges equals the number of inversions
		- inversion --> A comes after B but should be in from t of 
- Stable

shell sort


callback


v.compereTo(w) -> Comparable interface (natural order)
- negative integer if less
- 0 if equal
- positive if greater
- exception if incompatible types

Comparator -> alternative order (pass as second argument to sort)


Sorting algorithm properties
- Stability -> preserve relative order of items with equal keys (relative to original order)
- in-place -> if it uses <= log N extra memory

Computational complexity: framework to study efficiency of algorithms for solving a particular problem X

model of computation: allowable operations


cost model : operation counts

upper bound: cost guarantee provided by some algorithm for X
lower bound: proven limit on cost guarantee of all algorithms for X

optimal algorithm: algorithm with best possible cost guarantee for x


Any compare-based sorting algorithm must use at least lg(N!) ~ N lg N compares in the worst-case


mergesort
- top-down
	- divide array into two halves
	- recursively sort each half
	- merge two halves
- ~N/2 to n calls to less
- N lg N compares to sort an array of length N
- uses <= 6 N lg N array accesses
- Mergesort uses extra space proportional to N
	- in-place merge is possible but very difficult
	- aux of N/2 is easy
- mergesort is stable
	- takes from left subarray if equal keys, therefore never mixes equal keys order
- improvements
	- insertion sort for ~10 items is faster, just switch!
	- stop if already sorted (if largest item in first half <= smallest item in second half)
	- eliminate the copy to auxiliary, by switching the role of input and auxiliary array in each recursive call (saves time, not space)
- -bottom up merge sort
	- pass through array, merging subarrays of size 1, repeat for larger and larger subarrays (2, 4, 8, etc)



Natural merge sort - exploit pre-existing order by identifying naturally-occurring runs -> fewer passes vs. extra compares (TimSort)


Quicksort
- description
	- shuffle array
	- partition array so that for some j
		- entry a(j) is in place
		- no  larger entry to the left of j
		- no smaller entry to the right of j
	- sort each subarray recursively
- partitioning
	- repeat until i and j pointers cross
		- scan i from left to right so long as (a(i) < a(lo))
		- scan j from right to left so long as (a(j) > a(lo))
		- exchange a(i) with a(j)
- equal keys
	- it is better to stop scans on keys equal to the partitioning item's key
- time
	- N lg n best case
	- N^2/2 worst case -> but more likely that a lightning bolt strikes your computer during execution (if randomizing)
	- average case = 2(N + 1) ln N ~ 1.39 N lg N
- Properties
	- in-place (consttant time partitioning, log extra space for  recursion (with very high probability))
	- Unstable
- improvements
	- insertion sort small subarrays
	- best choice of pivot item = median, median of 3 random items is best
		- 12/ 7 N ln N compares
		- 12 / 35 N ln N exchanges


Quick-select
- Entry a(j) is in place, no larger entry to the left of j, no smaller entry to the right of j
- repeat in one subarray, depending on j, finished when j equals k
- takes linear time on average 
	- 2N compares
	- (2 + 2 ln 2) N ~ 3.38 N compares to find median
- context -> geometric series
	- still high worst-case
- qsort on equal keys
	- do not continue scans on equal keys (1/2N^2 compares)
	- stop scans on equal keys (N lg N)
	- put all equal keys in place (n compares when all equal keys)
		- dutch flag problem (dijskra) (3-way partitioning)
			- let v be a partitioning item a(lo)
			- (a(i) < v): exchange a(lt) with a(i): increment both lt and i)
			- (a(i) > v): exchange a(gt) with a(i): decrement gt
			- (a(i) == v) increment i

dual-pivot quicksort
- use two partitioning items 
	- keys less than p1
	- keys between p1 and p2
	- keys greater than p2
- basically a conditional way to add dijkstra's 3-way partitioning
	- repeat main loop until i and gt pointers cross
		- if (a(i) < a(lo)) exchange a(i) with a(lt) and increment lt and i
		- else if (a(i) > a(hi)) exchange a(i) with a(gt) anddecrement gt
		- else increment i


Geometric series



Algorithms
- dual-pivot quicksort for primitive types (faster)
- timsort for reference types (stable)


Collections
- data type that stores group of items
- Insert and delete items (specific ordering)
	- stack
	- queue
	- symbol table
	- set


Priority Queue
- find the largest M items in a stream of N items
- constraint : not enough memory to store N items
- implementation
	- binary heap
		- array representation of a heap-ordered complete binary tree

heap-ordered binary tree
- keys in nodes
- parent's key is no smaller than its children's keys
- array representation
	- indices start at 1
		- largest key is a(1)
	- take nodes in level order
	- no explicit links needed
	- parent of node at k is at k/2
	- children of node at k are at 2k and 2k+1
- swim
	- promote node, if becomes larger than parent
	- exchange key in child with key in parent
	- repeat until heap order restored
- Insertion
	- add node at end, then swim it up
	- at most 1+ lg N compares
- sink
	- demote in heap
	- exchange key in parent with key in larger child
	- repeat until heap ordered
- Del max
	- exchange root with node at end, then sink it down
	- at most 2 lg N compares
- bin heap properties
	- immutability of keys 8client does not change keys while they're in the PQ
- additional operations that could be implemented
	- remove arbitrary item
	- change priority of item
- Improvements
	- do half-exchanges in sink and swim
		- reduce number of array accesses


Multiway heap
- complete d-way tree
- parent's key no smaller than its children's keys
	- height of complete d-way tree on N nodes is log d N
	- sweet spot of d is 4
	- insert - log d (N)
	- del max - d log d N
	- max = 1 


Binary tree
- empty, or a node with links to left and right binary trees

complete tree
- perfectly balanced, except for bottom level
- Height of complete tree with N nodes is lg N
	- height only increases when N is a power of 2


Immutable- can't change the data type value once created
data type - set of values and operations on those values

Immutable data types
- String Integer, Double, Color, Vector, Transaction, Point2D
- why
	- simplifies debugging
	- safer in presence of hostile code
	- simplifies concurrent programming
	- safe to use as key in priority queue or symbol table
- why not
	- must create new object for each data type value

Mutable data types
- StringBuilder, Stack, Counter, Java array


heapsort
- basic plan for in-place sort
- view input array as a complete binary tree
- heap construction: build a max-heap with all N keys
- sortdown: repeatedly remove the maximum key
- Heap construction
	- build max heap using bottom-up method
- analysis
	- heap construction uses <= 2 N compares and exchanges
	- heapsort uses <= 2 N lg N compares and exchanges
		- can be improved to 1 N lg N
- properrties
	- in-place sorting algorithm with N log N worst-case
- optimal for both tima and space but
	- inner loop longer than quicksort's 
	- makes poor use of cache memory
	- not stable

merge sort in-place possible but not practical
N log N worst-case quicksort possible but not practical



Introsort
- as fast as quicksort in practice N log N in worst case
- run quicksort
- switch to heapsort if stack depth exceeds 2 lg N
- cutoff to insertion sort for N = 16


Symbol tables ST
- key-value pair abstraction
	- insert a value with a specified key
	- given a key, search for the corresponding value

Associative array
- init
- put(Key key, Value val)
- get(Key key)
- delete( Key key)
- contains(Key key)
- isEmpty()
- size()
- keys()
- Conventions
	- values are not Null
	- method get() returns null if key is not present
	- method put() overwrites old value with new value
	- why
		- easy to implement contains
		- lazy version of delet()
- Key assumptions
	- comparable with compareto
	- equals() works
	- hashCode() works
	- immutable



Equals
- reflexive x.equals(x) is true
- symmetrix x.equals(y) iff y.equals(x)
- transitive x.equals(y), y.equals(z), x.equals(z)
- non-null x.equals(null) is false


symbol table implementations
- two arrays, unordered 
	- bad
- ordered array of key-value pairs
	- ranked operations work
	- insertion is very slow


Binary search tree
- binary tree
- symmetric order : each node has a key, and every node's key is larger than all keys in its left subtree, smallr than all keys in its right subtree
- if less, go left, if greater, go right, if null, insert
- tree shape depends on order of insertion
- time
	- if n distinct keys are inserted into a bst in random order the expected number of compares for a serach/insert is ~2 ln N
		- expected heigh is ~4.311 ln N
	- worst case heigh is N
- ordered operations
	- max and min
	- floor and ceiling
	- rank and select
		- in eac hnode, we store the number of nodes in the subree rooted at that node, to implement size(), return the count at the root node 
- traversals
	- gives sorted order of keys in tree
- Deletion in BSt
	- lazy approach -> tombstone, set value to null
		- 2 ln n per insert, search and delete (if keys in random order)
	- Hibbard deletion
		- to delete node with key k, search for node t containing key k
		- delete t by setting parent link to null
		- to delete a node with key k: search for node t containing key k
		- delete 


correspondence between BSTs and quicksort partitioning is 1-1 if array has no duplicate keys



Skoða 1d range search (777)



orthagonal line segment intersection
- given N horizontal and vertical line segments, find all intersections
- nondegeneracy assumption: all x and y coordinates are distinct
- sweep line algorithm
	- sweep vertical line from left to right
	- x-coordinates define events
	- h-segment (left endpoint): insert y-coordinate into BST
- Skil EkkI hvernig viRKAR
	- takes time proportional to N log N + R
	- to find all R intersections among N orthogonal line segments
		- put x-coordinates on a PQ
		- insert y-coordinates into BST
		- delete y-coordinates from BSt
		- range searches in BST
	- sweep line reduces 2d orthogonal line segment intersection search to 1d range search



kd-tree (keys are points in the plane)
- ops
	- insert a 2d key
	- search 2d key
	- delete 2d key
	- range search: find all keys that lie in a 2d range
	- range count: number of keys that lie in a 2d range
- use a tree  to represent a recursive subdivision of 2d space
	- 2d tree: recursively divide space into two halfplanes
	- BSt but use x and y coordinates as key
	- search gives rectangle containing point
	- insert further subdivides the plane
	- Starts at left right, then up down, then repeat
		- down is left, up is right
- Range search
	- check if point in nodes lie in given rectangle
	- recursively search left/bottom (if any could fall in rectangle)
	- recursively search right/top (if any could fall in rectangle)
		- typical case R + log N
		- worst case (assuming the tree is balanced) R + sqrt(N)
- nearest neighbor
	- find closest point to query point
		- check distance from point in node to query point
		- recurrsively search left/bottom (if it could contain a closer point)
		- recursively search right/top (if ti could contain a closer point)
		- organize method so that it begins by searching for query point
	- time
		- log N typically
		- worst case N (even if tree is balanced)



2-3 tree
- allow 1 or 2 keys per node
- 2-node: one key, two children
- 3-node: two keys, three children
- Symmetric order: inorder traversal yields keys in ascending order
- perfect balance: every path from root to null link has same length
- insertion
	- add new key to 3-node to create temporary 4-node
	- move middle key in 4-node into parent
	- repeat up the tree as necessary
	- if you reach the root and it's a 4-node split it into three 2 nodes
- height in the worst case is lg  N
	- best case is log 3 N ~ 0.631 lg N
- guaranteed logarithmic performance for search and insert


LLRB
- left leaning red-black tree
- equivalent to 2-3 trees
- internal left-leaning links as glue for 3-nodes
- BST such that 
	- No node has two red links connected to it
	- every path form root to null link has the same number of black links
	- red links lean left
- algorithms
	- search is same as for elementary BST
	- left rotation (then right rot)
		- orient a right-leaning red link to lean left
	- color flip
		- recolor to split a 4-node
	- insertion
		- maintain 1-1 correspondence with 2-3 trees by applying elementary red-black BST operations
		- all insertions are connected with a red link
- height
	- <= 2 lg N in the worst case
	- height is ~ lg N in typical applications


B-trees
- generalize 2-3 trees by allowing up to M-1 key-link pairs per node
	- at least 2 key-link pairs at root
	- at least M/2 key-link pairs in other nodes
	- external nodes contain client keys
	- internal nodes contain copies of keys to guide search
- Search
	- start at root
	- find interval for search key and take corresponding link
	- search terminates in external node
- insertion
	- search for new key
	- insert at bottom
	- split nodes with m key-link pairs on the way up the tree
- balance
	- a search or insertion in a b-tree of order M iwth N keys requries between log M-1 N and log M/2 N probes
		- all internal nodes besides root, have between M/2 and M -1 links
- when
	- for files systems and databases


Hash tables
- hash function - compute array index from key
- issues
	- compute hash function
	- equality test
	- collision resolution


Horner's method to hash string of length L
- h = s(0) * 31^L-1 + ... s(L-1) * 31^0


uniform hashing assumption
- each key is equally likely to hash to an integer between 0 and M-1

expect every bin has >= 1 ball after ~ M ln M tosses
After M tosses, expect most loaded bin to have theta(log M / log log M) balls

collision: two distinct keys hashing to same index

separate chaining symbol table
- use an array of M < N linked lists
	- bins
- typical cohise M ~ N/5 -> ~ constant-time operations
- resizing
	- Double size of array M when N/M >= 8
	- halve size of array M when N/M <= 2
	- (need to rehash all keys when resizing)
- deleting key
	- just link past it (if linked list)
	- else tombstone and fix later is nice
- two-probe hashing
	- two hash, insert to shorter

Linear probing -> is open addressing
- two arrays
- when key collised, find next empty slot and put it there
- Array size M must be greater than the number of key value pairs N
- typical choice alpha = N/M ~ 1/2
- resizing
	- doulbe size of array M when N/M >= 1/2
	- Halve size of array M when N/M <= 1/8
	- (need to rehash all keys when resizing)
- deletion
	- add tombstone
- double hashing
	- skip a variable amount, not just 1 each time (eliminate clustering)

hash tables
- for unordered keys - faster for simple keys

balanced search trees
- stronger performance guarantee
- support for ordered ST operations

cuckoo hash
- two ararys, with different hash functions
- place an element in either of its allocated slots
- if both slots are full, kick one out and let it find a new place
- insertion may fail, if loop, probability of this is low if m < n/2
- time
	- search O(1) deterministic
	- insert O81) expected


symbol tables for sparce vectors

(939) good

Path : sequence of vertices connected by edges
cycle : path whose first and last vertices are the same
degree: the number of edges connected to a vertex
- indegree
- outdegree


set of edges
adjacency-matrix graph representation
- for each v-w in graph adj(v)w) = ad(w)(v) = true
adjacency-list graph representation
- vertex-indexed array of lists
- - use this, real world graphs tend to be sparse

depth-first search -- DFS
- mark v as visited (stack)
- recursively visit all unmarked vertices w adjacent to v
	- find all vertices connected to a given source vertex
	- find a path between two vertices
- boolean() marked to mark visited vertices
- int() edgeTo - a parent-link representation of a tree rooted at s
- edgeTo(w) == v, means the edge v-w taken to visit w for the first time
- time
	- dfs marks all vertices connected to s in time proportional to the sum of their degrees
		- each vertex connected to s is visited once

bredth-first search BFS
- repeat until queue is empty
	- remove vertex v from queue
	- add to queue all unmarked vertices adjacent to v and mark them
- marked()
- edgeto()
- distTo()
- when
	- find path from s to t that uses fewest number of edges
- how
	- put s into FIFO queue and mark s as visited
	- repeat until the queue is empty
		- remove the least recently added vertex v
		- add each of v's unvisited neighbors to the queue and mark them as visited
- why work -> examine vertices in increasing distance from s


Connected component - a maximal set of connected vertices
- vertices v and w are connected if there is a path between them
- preprocess the graph to asnwer queries of the form is v connected to w
	- initialize all vertices v as unmarked
	- for each unmarked vertex v, run dfs to identify all vertices discovered as part of the same component
- marked()
- id()
- count


is a graph bipartite: solvable (DFS)
find a cycle: (DFS)
find a general cycle that uses every edge exactly once: doable
lay out a graph in the plane without crossing edges: expert
find a cycle that visits every vertex exactly once: intractable
are two graphs identical except vertex names: no one knows


directed graphs
- set of vertices connected pairwise by directed edges


topological sort


DAG: directed acyclic graph

topological sort
- run depth-first search
- return vertices in reverse postorder
	- add to stack, right after exploring every vertex in the adjacency list

dfs
- preorder: order in which dfs() is called
- postorder: order in which dfs() returns


Strong connectivity
- vertices v and w are strongly connected if there is both a directed path from v to w and a directed path from w to v
- strong component
	- a maximal subset of strongly-connected vertices
- kosarju-sharir algorithm
	- phase1: compute reverse postorder in reverse of G
	- phse2: run dfs in G, visiting unmarked vertices in reverse postorder of Gr
	- time
		- E + V


Minimum spanning tree


spanning tree
- of G is a subgraph T that is 
	- connected
	- acyclic
	- includes all of the vertices
- Minimum spanning tree
	- given undirected graph g with positive edge weights
	- find a min weight spanning tree
- algorithms
	- greedy
		- start with all edges colored gray
		- find cut with no black crossing edges; color its min-weight edge black
		- repeat until V-1 edges are colored black
	- Kruskal's algorithm
		- consider edges in ascending order of weight
		- add next edge to tree t unless doing so would create a cycle
			- use union find (vertices) and priority queue (edges)
	- Prim's algorithm
		- start with vertex 0 and greedily grow tree T
		- add to T the min weight edge with exactly one endpoint in T
		- repeat until V-1 edges
		- lazy solution
			- maintain PQ of edges with at least one endpoint in T
			- key = edge: priority = weight of edge
			- delete-min to determine next edge e = v-w to add to T
			- disregard if both endpoints v and w are marked (both in T)
			- otherwise let w be the unmarked vertex (not in T)
				- add to PQ any edge incident to w (assuming other endpoint in T)
				- add e to T and mark W
		- eager implementation
			- extra space at most V, running time E log V

would adding edge v-w to tree T create a cycle, if not add it.
- use union-find, WQU
	- add vertices to this data structure, if they are already connected, then connecting them would create a cycle

cut property
- a cut in a graph is a partition of its vertices into two nonempty sets
- a crossing edge connects a vertex in one set with a vertex in the other
- given any cut, the crossing edge of min weight is in the mst


maximum spanning tree,
- given and edge weighted graph g, find the spanning tree that maximizes the sum of the edge weights -> just reverse


minimum bottleneck spanning tree
- given an edge weighted graph G, find a spanning tree that minimizes the maximum weight of its edges
	- the maximal edge is as cheap as possible


dynamic programming
- fara aðeins betur yfir þetta shit

skoða heap sort

resizing in hash table