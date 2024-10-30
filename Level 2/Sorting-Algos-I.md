# Sorting Algos I

- [Selection Sort](#selection-sort)
- [Bubble Sort](#bubble-sort)
- [Insertion Sort](#insertion-sort)
- [Divide and Conquer Algorithms](#divide-and-conquer-algorithms)
- [Merge Sort](#merge-sort)
- [Divide and Conquer Exercises](#exercises)

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

    while (i < n1 && j < n2) {
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

## Divide and Conquer Exercises

1. [Merge Sort](https://leetcode.com/problems/sort-an-array/)
2. [Merge K Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
3. [Longest Nice Substring](https://leetcode.com/problems/longest-nice-substring/)
