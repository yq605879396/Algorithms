## Algorithms - 2 Data Structures



[TOC]

#### Data Structure

DS is a way to store and organize data in order to facilitate access and modifications

#### Basic Abstract Data Types (ADTs)

A mathematical model of the data methods used to modify and access the data
we don't care the implementation

##### list

##### stack

>  PUSH(S,x), POP(S)

##### queue

> ENQUEUE(Q,x), DEQUEUE(Q)
> Q.head, Q.tail, Q.length
>
> ###### Priority queue
>
> > data with a key
> > INSERT(P,x), EXTRACT-MAX(P), MAX(P), INCREASE-KEY(P,x,k)
> >
> > Applications: OS(manage jobs), Graph Algorithms(Dijkstra), arrange events, compression(Huffman encoding), heapsort...
> >
> > How should we implement the priority queue:
> > binary heap,..

##### set

##### dictionary

#### Common data structures

##### heap

> **Binary Heap**
>
> > **structure**
> > https://cs.stackexchange.com/questions/841/proving-a-binary-heap-has-lceil-n-2-rceil-leaves
> >
> > > array structure, visualized as nearly complete tree(only the left of last layer may be not full)
> > >
> > > root-A[1], PARENT(i) = i/2, LEFT(i)= 2i, RIGHT(i)=2i+1
> > > attributes: A.length
> > >
> > > Theorem: A nearly complete binary tree of n nodes has height $\theta(logn)$
> > > prove:
> > >
> > > > a complete binary tree with height h has $\sum_{i=0}^h 2^i = \frac{1-2^{h+1}}{1-2} =2^{h+1}-1$ nodes
> > > > so for a nearly complete tree $1+ \sum_{i=0}^{h-1} 2^i=2^h \leq n \leq 2^{h+1} -1$
> >
> > **Attribute**
> >
> > > min binary heap PARENT(A[i]) $\leq$ A[i]
> >
> > **Operations** - e.g. Min-heap
> >
> > > ```pseudocode
> > > HEAP-MINIMUM(A)
> > > 	return A[1]
> > > 
> > > HEAP-EXTRACT-MIN(A)
> > > 	if A.heap-size < 1
> > > 		error 'heap underflow'
> > > 	min = A[1]
> > > 	A[1] = A[A.heap-size]
> > > 	A.heap-size = A.heap-size - 1
> > > 	MIN-HEAPIFY(A, 1)
> > > 	return min
> > > 	
> > > MIN-HEAP-INSERT(A, key)
> > > 	A.heap-size = A.heap-size + 1
> > > 	A[A.heap-size] = inf
> > > 	HEAP-DECREASER-KEY(A, A.heap-size, key)
> > > 
> > > HEAP-DECREASE-KEY(A,i,key)
> > > 	if key > A[i]
> > > 		error 'new key is larger'
> > > 	A[i] = key
> > >     	while i > 1 and A[PARENT(i)] > A[i]
> > > 		exchange A[i] with A[PARENT(i)]
> > > 		i = PARENT(i)
> > > 	
> > > BUID-MIN-HEAP(A)
> > > 	A.heap-size = A.length
> > > 	for i = floor(A.length/2) downto 1
> > > 		MAX-HEAPIFY(A,i)
> > > 		
> > > MIN_HEAPIFY(A,i)
> > > 	l = LEFT(i)
> > > 	r = RIGHT(i)
> > > 	if l <= A.heap-size and A[l] < A[i]
> > > 		smallest = l
> > > 	else smallest = i
> > > 	if r <= A.heap-size and A[r] < A[smallest]
> > > 		smallest = r
> > > 	if smallest != i:
> > > 		exchange A[i] and A[smallest]
> > > 		MIN-HEAPIFY(A, smallest)
> > > 		
> > > HEAPSORT(A) #O(nlogn)
> > > 	BUILD-MAX-HEAP(A)
> > > 	for i = A.length downto 2
> > > 		exchange A[l] with A[1]
> > > 		A.heap-size == A.heap-size - 1
> > > 		MAX-HEAPIFY(A, 1)
> > > ```
> > >
> > > Time complexity of build a heap: O(n)
> > >
> > > > Amortized analysis: determine worst-case of a sequence of data structure operations
> > > >
> > > > | layer | height | depth | nodes       | time = relate node*c |
> > > > | ----- | ------ | ----- | ----------- | -------------------- |
> > > > | 1     | 3      | 0     | 1 = $2^0$   | $c\cdot 3\cdot 2^0$  |
> > > > | 2     | 2      | 1     | 2 = $2^1$   | $c\cdot 2\cdot 2^1$  |
> > > > | 3     | 1      | 2     | 4 = $2^2$   | $c\cdot 1\cdot 2^0$  |
> > > > | 4     | 0      | 3     | <=8 = $2^3$ |                      |
> > > >
> > > > h is the height of the tree
> > > > $T(n)\leq c \sum_{i=1}^{h} 2^{h-i}\cdot i \leq c\cdot s^h \sum_{i=1}^h s^{h-i}\cdot i \leq c\cdot 2^{logn}\sum_{i=1}^h 2^{-i}\cdot i\cdot\leq cn\sum_{i=1}^\inf 2^{-i}\cdot i$ 
> > > > $= cn\sum_{i=1}^{inf} (\frac 1 2)^i\cdot i = \frac{cn}{2} \sum_{i=1}^{inf} i \cdot(\frac 1 2)^{i-1} = \frac{cn}{2} \frac{1}{(1-1/2)^2} = O(n)$
> > > > notice that: 
> > > > $\frac{\partial \sum_{i=0}^{inf}x^i }{\partial x} = \sum_{i=0}^{inf}i\cdot x^{i-1}$
> > > > $\frac{\partial \frac{1}{1-x} }{\partial x} = \frac{1}{(1-x)^2}$
> > > > $\sum_{i=0}^{inf}x^i=\frac{1}{1-x}$

##### array

##### Hash

> **dictionary data structure**
>
> > universe of keys u
> > a data structure that stores a subset S \in u
> > operations:
> > SEARCH(S,k)
> > INSERT(S,x)
> > DELETE(S,x)
>
> **How should we implement the dictionary**
>
> > sorted array? linklist?
>
> ###### Hashing and Hash Tables
>
> > h(k)
> >
> > Collision
> >
> > > separate chaining: linklist
> > >
> > > Assumption:
> > >
> > > > Simple uniform hashing: any key is equally likely to hash to any of the m slots
> > > > for all $i \neq j, pr[h(k_i)=h(k_j)] = \frac{1}{m}$
> > >
> > > Analysis for unsuccessful search
> > >
> > > > $C_{x,y} = 1\ if \ h(x)= h(y)\ else\ 0 $
> >
> > choosing a hash function
> >
> > 
> >
> > fundamental weakness
> > for any hash function,  we can find a set of keys that are hashed to the same spot 
>
> ###### Universal Hashing:
>
> > **Universal Class of Hash Functions:**
> >
> > > $H = {h_1,h_2,...,h_w}$ is a universal hash function family if for all $k,k' \in U, Pr_{h\in H}[h(k) = h(k')\leq \frac{1}{m}],m$ is the table size
> >
> > **How to construct a universal Hash functions family:**
> >
> > > $H_{pm} = \lbrace  h_{a,b} (x) = ((ax+b)\ mod\ p)\ \rbrace  \ 1\leq a\leq p-1, 0 \leq b \leq p-1,\ and \ p\geq all\ keys$
> > >
> > > Proof:
> > >
> > > 1. If $h_{ab}(k) = h_{ab}(l)$ it is because they collided after mod p or mod m
> > > 2. If $h_{ab}(k) = h_{ab}(l)$ it is because they collided after  mod m
> > > 3. There is a 1-1 correspondence between the (r,s) pairs and the (a,b) pairs
> > >
> > >
> > >  
> > >
> >
> > **Theorem**
> >
> > > If  for all $k,k' \in U, Pr_{h \in H}[h(k)=h(k')]\leq\frac{1}{m}$, then for any $S \subseteq U$, for any $x \in U-S$ the expected number of collisions between x and the other elements in S is at most n/m, when |S|=n
> > >
> > > Proof:
> > >
> > >
> > > Corollary 1: If  for all $k,k' \in U, Pr_{h \in H}[h(k)=h(k')]\leq\frac{1}{m}$, then for any $S \subseteq U$, for any $x \in U-S$ thee expected number of comparisons for a successful search is O(1+n/m) and for an unsuccessful search is O(n/m) where |S| = n.
> > >
> > > Corollary 2: Using universal hashing and collision resolution by chaining in an initially empty table with m slots, it takes expected time $\theta (n)$ to handle any sequence of  n INSERT, SEARCH, and DELETE operations containing O(m) INSERT operations where m is the table size
> >
> > 
>
> ##### Perfect Hashing
>
> > Given a fixed set of n keys we can construct a static hash table of size $m=\theta(n)$ such that search takes $\theta (1)$ time in the worst case
> >
> > > **Theorem:**
> > > Hashing n keys into m = n*n slots using $h \in_R H$ then E(# collisions ) <  1/2
> > >
> > > **Proof:**
> > > probability that two keys collide is $1/m = 1/n^2$, and  # pairs of key = $\left(n \  2\right)$
> > > E(# collisions) $\leq (n\ 2) \cdot \frac{1}{n^2} = \frac{n(n-1)}{2} \cdot \frac{1}{n^2}<\frac {1}{2}$
> > >
> > > **Corollary:** 
> > > Probability of no collisions > 1/2
> > > Proof:  X be a R.V. holding the number of collisions, according to Markov inequality:
> > > $ Pr[X\geq 1] \leq \frac{E[X]}{1} < \frac{1}{2}$
> > > (FYI: Markov's inequality can refer to ....)
> >
> > To reduce the space: two levels
> >
> > > **Theorem:** 
> > > Let m=n be the size of the hash table at level 1
> > > Let n_j^2 be the size of the hash table at index j
> > > Let h be randomly chosen from a universal set H
> > > Then $Pr [\sum_{j=0}^{m-1} (n_j)^2 \geq 4n] < 1/2$
> > >
> > > **Proof:**
> > > the number of pairs that collide at the first layer:
> > > $\sum_{j=0}^{m-1}\sum_{x\in S_j} \sum_{y\in S_j} C_{x,y} = \sum_{x \in S} \sum_{y \in S_{h(x)} C_{x,y} = \sum}$
> > >
> > > $E[\sum_{j=0}^{m-1} n_i^2] = E[\sum_{x\in S} \sum_{y \in S}C_{xy}] =n + \sum_{x \in S} \sum_{y \in S-x} E[C_{xy}] \leq n + n(n-1)/m < 2n$
> > > Markov's inequality: $Pr[\sum_{i=1}^{m-1}(n_i)^2 \geq 4n] < 2n/4n = 1/2$
> >
> > 
>
> 
>
> 

##### tree

