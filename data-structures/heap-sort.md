---
description: >-
  Heap sort is a method of sorting that involves a max heap (heaps notes for
  more)
---

# Heap Sort

#### Heaps Review:

{% content-ref url="heaps.md" %}
[heaps.md](heaps.md)
{% endcontent-ref %}

#### Heap Sort Description

Heap sort is a method of sorting that takes advantage of the max heap data structure.  Conceptually, the heap sort procedure is to put all elements in a collection into a max heap using the heap rules (see "heaps" for more).  Next, the max item it removed from the max heap and put at the end of a new collection.  The heap is reformatted appropriately, and the procedure is repeated n times for n elements.

#### Heap Sort Time/Space Complexity Analysis

The runtime of heap sort follows closely with the runtime of creating and removing from a heap.  When building the heap each item is considered once to put into the heap.  Then, while inserting into the heap, a max of log(n) levels must be visited before insertion.  While removing there are again n elements to remove, and the levels of the heap amount to max log(n).  Thus it follows that the time complexity of heap sort is O(n log n).&#x20;

When considering the space complexity it can be observed that an entire max heap must be constructed and kept in memory.  This means at least linear space is required for heap sort, plus some possible extra memory allocated to pointers between nodes, etc.  One possible way to get rid of this extra memory is to do heap sort in place.  Instead of making a new heap, the elements are of the heap are represented in their array representation (see "heaps" for more).  Again, the runtime is kept at O(n log n), but the space is reduces to be constant.

#### Heap Sort Java Implementation:

```
// Java program for implementation of Heap Sort
public class HeapSort {
	public void sort(int arr[])
	{
		int n = arr.length;

		// Build heap (rearrange array)
		for (int i = n / 2 - 1; i >= 0; i--)
			heapify(arr, n, i);

		// One by one extract an element from heap
		for (int i = n - 1; i > 0; i--) {
			// Move current root to end
			int temp = arr[0];
			arr[0] = arr[i];
			arr[i] = temp;

			// call max heapify on the reduced heap
			heapify(arr, i, 0);
		}
	}

	// To heapify a subtree rooted with node i which is
	// an index in arr[]. n is size of heap
	void heapify(int arr[], int n, int i)
	{
		int largest = i; // Initialize largest as root
		int l = 2 * i + 1; // left = 2*i + 1
		int r = 2 * i + 2; // right = 2*i + 2

		// If left child is larger than root
		if (l < n && arr[l] > arr[largest])
			largest = l;

		// If right child is larger than largest so far
		if (r < n && arr[r] > arr[largest])
			largest = r;

		// If largest is not root
		if (largest != i) {
			int swap = arr[i];
			arr[i] = arr[largest];
			arr[largest] = swap;

			// Recursively heapify the affected sub-tree
			heapify(arr, n, largest);
		}
	}

	/* A utility function to print array of size n */
	static void printArray(int arr[])
	{
		int n = arr.length;
		for (int i = 0; i < n; ++i)
			System.out.print(arr[i] + " ");
		System.out.println();
	}

	// Driver code
	public static void main(String args[])
	{
		int arr[] = { 12, 11, 13, 5, 6, 7 };
		int n = arr.length;

		HeapSort ob = new HeapSort();
		ob.sort(arr);

		System.out.println("Sorted array is");
		printArray(arr);
	}
}

```

#### Heap Sort Drawbacks/Why don't we regularly use Heap Sort?

Heap sort has problems with bad caching (you know the drill).
