Selection Sort

	[3, 6, 1, 3, 7, 2, 9]
	[1| 6, 3, 3, 7, 2, 9]
	[1, 2| 3, 3, 7, 6, 9]
    [1, 2, 3| 3, 7, 6, 9]
    [1, 2, 3, 3| 7, 6, 9]
    [1, 2, 3, 3, 6| 7, 9]
    [1, 2, 3, 3, 6, 7| 9]
    [1, 2, 3, 3, 6, 7, 9]	
	
	void selectionSort(int[] array) {
		if (array == null || array.length < 2) {
			return;
		}
		for (int i = 0; i < array.length; i++ ) {
			int minIndex = i;
			for (int j = i; j < array.length; j++) {
				if (array[j] < array[minIndex]) {
					minIndex = j;
				}
			}
			swap(array, i, minIndex);
		}
	}
	
	void swap(int[] array, int i, int j) {
		int temp = array[i];
		array[i] = array[j];
		array[j] = temp;
	}

Insertion Sort
Quick Sort
Merge Sort
Radix Sort
Topological Sort
Tree Depth-First Search (Pre-, In-, Post-Order)
Tree Breadth-First Search
Graph Depth-First Search
Graph Breadth-First Search
Dijkstra's Shortest Path
Unweighted Graph Shortest Path
Knapsack 0/1
Knapsack Unbounded
Sieve of Eratosthenes

A*
Bellman-Ford
Bloom-Filter
Convex Hull
Fisher-Yates Shuffle
Kruskal's
Max Flow
Prim's
Rabin-Karp
Traveling Salesman
Union Find