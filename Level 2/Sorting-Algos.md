# Sorting Algos

- [Selection Sort](#selection-sort)
- [Bubble Sort](#bubble-sort)
- [Insertion Sort](#insertion-sort)
- [Divide and Conquer Algorithms](#divide-and-conquer-algorithms)
- [Merge Sort](#merge-sort)
- [Heap Sort](#heap-sort)
- [Quick Sort](#quick-sort)

## Selection Sort

**Best Case Time Complexity**: O(n^2)
**Worst Case Time Complexity**: O(n^2)
**Average Case Time Complexity**: O(n^2)

Selection Sort is an in-place comparison sorting algorithm that divides the input array into two parts: the subarray of items already sorted and the subarray of items remaining to be sorted.

How it works:

1. Find the minimum element in the array.
2. Swap the minimum element with the first element.
3. Repeat the process for the remaining elements.

```cpp

void selectionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        swap(arr[i], arr[minIndex]);
    }
}

```

## Bubble Sort

**Best Case Time Complexity**: O(n)
**Worst Case Time Complexity**: O(n^2)
**Average Case Time Complexity**: O(n^2)

Bubble Sort is the simplest sorting algorithm that works by repeatedly swapping the adjacent elements if they are in the wrong order.

How it works:

1. Start from the first element, compare it with the next element.
2. If the first element is greater than the next element, swap them.
3. Repeat the process for all the elements in the array.
4. Repeat the process for n-1 times.

```cpp

void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

```

## Insertion Sort

**Best Case Time Complexity**: O(n)
**Worst Case Time Complexity**: O(n^2)
**Average Case Time Complexity**: O(n^2)

Insertion Sort is a simple sorting algorithm that builds the final sorted array one item at a time.

How it works:

1. Start from the second element, compare it with the previous elements.
2. If the current element is smaller than the previous element, shift the previous element to the right.
3. Repeat the process for all the elements in the array.

```cpp

void insertionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

```

## Divide and Conquer Algorithms

Divide and Conquer is a powerful algorithm design paradigm that breaks a problem into smaller subproblems, solves the subproblems recursively, and then combines the solutions to the subproblems to solve the original problem.

The three steps of the Divide and Conquer algorithm are:

1. Divide: Break the problem into smaller subproblems.
2. Conquer: Solve the subproblems recursively.
3. Combine: Combine the solutions to the subproblems to solve the original problem.

Divide and Conquer algorithms are often used to solve problems that can be broken down into smaller subproblems that are similar to the original problem.

Examples of Divide and Conquer algorithms include Merge Sort, Quick Sort, and Binary Search.

Example Code:

```cpp

void divideAndConquer(vector<int>& arr, int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;
        divideAndConquer(arr, l, m);
        divideAndConquer(arr, m + 1, r);
        // Combine the solutions to the subproblems
    }
}

```

## Merge Sort

**Best Case Time Complexity**: O(n log n)
**Worst Case Time Complexity**: O(n log n)
**Average Case Time Complexity**: O(n log n)

Merge Sort is a divide and conquer algorithm that divides the input array into two halves, recursively sorts the two halves, and then merges the sorted halves.

How it works:

1. Divide the array into two halves.
2. Recursively sort the two halves.
3. Merge the two sorted halves.

```cpp

void merge(vector<int>& arr, int l, int m, int r) {
    int n1 = m - l + 1;
    int n2 = r - m;

    vector<int> L(n1), R(n2);

    for (int i = 0; i < n1; i++) {
        L[i] = arr[l + i];
    }

    for (int i = 0; i < n2; i++) {
        R[i] = arr[m + 1 + i];
    }

    int i = 0, j = 0, k = l;

    while (i < n1 && j < n2) { // merge two halves
        if (L[i] <= R[j]) {
            arr[k++] = L[i++];
        } else {
            arr[k++] = R[j++];
        }
    }

    while (i < n1) {
        arr[k++] = L[i++];
    }

    while (j < n2) {
        arr[k++] = R[j++];
    }

}


void mergeSort(vector<int>& arr, int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);
        merge(arr, l, m, r);
    }
}

```

-Solve: [Merge K Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

## Heap Sort

### Heap

A heap is a complete binary tree that satisfies the heap property. The heap property states that the key of each node is either greater than or equal to (max heap) or less than or equal to (min heap) the keys of its children.

A heap can be represented as an array, where the parent of the node at index `i` is at index `(i - 1) / 2`, and the children of the node at index `i` are at indices `2 * i + 1` and `2 * i + 2`.

### Heapify

Heapify is an operation that maintains the heap property by moving the node at index `i` down the tree until the heap property is satisfied.

```cpp

void heapify(vector<int>& arr, int n, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < n && arr[left] > arr[largest]) {
        largest = left;
    }

    if (right < n && arr[right] > arr[largest]) {
        largest = right;
    }

    if (largest != i) {
        swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}

```

### Heap Sort

**Best Case Time Complexity**: O(n log n)
**Worst Case Time Complexity**: O(n log n)
**Average Case Time Complexity**: O(n log n)

Heap Sort is a comparison-based sorting algorithm that uses a binary heap data structure to sort an array.

How it works:

1. Build a max heap from the array.
2. Swap the root node with the last node and heapify the remaining nodes.
3. Repeat the process for the remaining nodes.

```cpp
void heapSort(vector<int>& arr) {
    int n = arr.size();

    for (int i = n / 2 - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }

    for (int i = n - 1; i > 0; i--) {
        swap(arr[0], arr[i]);
        heapify(arr, i, 0);
    }
}
```

## Quick Sort

### Quick Select

What is Quick Select?

Quick Select is a selection algorithm that selects the kth smallest element from an unsorted array in expected linear time.

How does it work?

1. Choose a pivot element from the array.
2. Partition the array into two subarrays such that all elements less than the pivot are on the left and all elements greater than the pivot are on the right.
3. If the pivot is at index k, return the pivot.

```cpp

int quickSelect(vector<int>& arr, int l, int r, int k) {
    if (l == r) {
        return arr[l];
    }

    int pivot = arr[l + (r - l) / 2];
    int i = l;
    int j = r;

    while (i <= j) {
        while (arr[i] < pivot) {
            i++;
        }

        while (arr[j] > pivot) {
            j--;
        }

        if (i <= j) {
            swap(arr[i], arr[j]);
            i++;
            j--;
        }
    }

    if (k <= j) {
        return quickSelect(arr, l, j, k);
    }

    if (k >= i) {
        return quickSelect(arr, i, r, k);
    }

    return arr[k];
}

```

### Quick Sort

**Best Case Time Complexity**: O(n log n)
**Worst Case Time Complexity**: O(n^2)
**Average Case Time Complexity**: O(n log n)

Quick Sort is a comparison-based sorting algorithm that uses a divide and conquer strategy to sort an array.

How it works:

1. Choose a pivot element from the array.
2. Partition the array into two subarrays such that all elements less than the pivot are on the left and all elements greater than the pivot are on the right.
3. Recursively sort the two subarrays.

```cpp

void quickSort(vector<int>& arr, int l, int r) {
    if (l < r) {
        int pivot = arr[l + (r - l) / 2];
        int i = l;
        int j = r;

        while (i <= j) {
            while (arr[i] < pivot) {
                i++;
            }

            while (arr[j] > pivot) {
                j--;
            }

            if (i <= j) {
                swap(arr[i], arr[j]);
                i++;
                j--;
            }
        }

        quickSort(arr, l, j);
        quickSort(arr, i, r);
    }
}

```
