##Mystical Lexical Order
	Given a sorted list of words, infer the ordering of the alphabet. The language is unknow.
	Example :
	Input:  words[] = {"baa", "abcd", "abca", "cab", "cad"}
	Output: Order of characters is 'b', 'd', 'a', 'c'
	Note that words are sorted and in the given language "baa"
	comes before "abcd", therefore 'b' is before 'a' in output.
	Similarly we can find other orders.

####思路
	What data structure?
	topological order (sort)
	graph
	b a c

	b ->a
	d ->a
	a->c
	b->d

	input words[] = {}
	non-indegree-> firstnode

	queue

	decrese its indegree
	BFS traversal
