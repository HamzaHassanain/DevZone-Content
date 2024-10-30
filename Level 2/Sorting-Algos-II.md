# Sorting Algos II

- [Heap Sort](#heap-sort)
- [Quick Sort](#quick-sort)
- [Counting Sort](#counting-sort)
- [Radix Sort](#radix-sort)

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

## Counting Sort

**Best Case Time Complexity**: O(n + k)
**Worst Case Time Complexity**: O(n + k)
**Average Case Time Complexity**: O(n + k)

Where K is the range of the non-negative key values.

Here, keep in mind that Counting Sort is not a comparison-based sorting algorithm.
It is optimal for sorting integers with a small range of values.

Counting Sort is a non-comparison-based sorting algorithm that sorts an array by counting the number of occurrences of each element and using this information to place the elements in the correct order.

How it works:

1. Count the number of occurrences of each element in the array.
2. Calculate the prefix sum of the counts.
3. Place the elements in the correct order based on the prefix sum.

```cpp

void countingSort(vector<int>& arr) {
    int n = arr.size();
    int maxVal = *max_element(arr.begin(), arr.end());
    vector<int> count(maxVal + 1);
    vector<int> output(n);

    for (int i = 0; i < n; i++) {
        count[arr[i]]++;
    }

    for (int i = 1; i <= maxVal; i++) {
        count[i] += count[i - 1];
    }

    for (int i = n - 1; i >= 0; i--) {
        output[count[arr[i]] - 1] = arr[i];
        count[arr[i]]--;
    }

    for (int i = 0; i < n; i++) {
        arr[i] = output[i];
    }
}

```

## Radix Sort

**Best Case Time Complexity**: O(nk)
**Worst Case Time Complexity**: O(nk)
**Average Case Time Complexity**: O(nk)

Where k is the number of digits in the maximum number.

Radix Sort is a non-comparison-based sorting algorithm that sorts an array by sorting the elements based on their individual digits.

How it works:

1. Find the maximum number in the array.
2. For each digit position, sort the elements based on that digit using Counting Sort.

```cpp

void countingSort(vector<int>& arr, int exp) {
    int n = arr.size();
    vector<int> count(10);
    vector<int> output(n);

    for (int i = 0; i < n; i++) {
        count[(arr[i] / exp) % 10]++;
    }

    for (int i = 1; i < 10; i++) {
        count[i] += count[i - 1];
    }

    for (int i = n - 1; i >= 0; i--) {
        output[count[(arr[i] / exp) % 10] - 1] = arr[i];
        count[(arr[i] / exp) % 10]--;
    }

    for (int i = 0; i < n; i++) {
        arr[i] = output[i];
    }
}


void radixSort(vector<int>& arr) {
    int maxVal = *max_element(arr.begin(), arr.end());
    
    for (int exp = 1; maxVal / exp > 0; exp *= 10) {
        countingSort(arr, exp);
    }
}

```
