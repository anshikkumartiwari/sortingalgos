
# Sorting Algorithms in C

This repository contains C implementations of six different sorting algorithms. Each algorithm is unique in its approach and has different time complexities. Below, you'll find a brief explanation of each algorithm, when to prefer it, and the corresponding C code.

## 1. Insertion Sort

**Unique Feature:** Builds the final sorted array one item at a time, making it efficient for small or nearly sorted arrays.

**Time Complexity:** O(n^2) in the worst case, O(n) in the best case (nearly sorted array).

**When to Use:** Prefer it when the array is small or nearly sorted.

```c
void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}
```

## 2. Selection Sort

**Unique Feature:** Selects the smallest (or largest) element from the unsorted portion and swaps it with the first unsorted element.

**Time Complexity:** O(n^2) regardless of the input.

**When to Use:** Useful when memory writes are more expensive than comparisons.

```c
void selectionSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        int min_idx = i;
        for (int j = i+1; j < n; j++) {
            if (arr[j] < arr[min_idx])
                min_idx = j;
        }
        int temp = arr[min_idx];
        arr[min_idx] = arr[i];
        arr[i] = temp;
    }
}
```

## 3. Bubble Sort

**Unique Feature:** Repeatedly swaps adjacent elements if they are in the wrong order, "bubbling" the largest unsorted element to its correct position.

**Time Complexity:** O(n^2) in the worst case, O(n) in the best case (if already sorted).

**When to Use:** Useful for educational purposes or when the array is small and nearly sorted.

```c
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        int swapped = 0;
        for (int j = 0; j < n-i-1; j++) {
            if (arr[j] > arr[j+1]) {
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
                swapped = 1;
            }
        }
        if (swapped == 0) {
            break;
        }
    }
}

```

## 4. Counting Sort

**Unique Feature:** Counts the number of occurrences of each unique element in the array, then uses these counts to place elements in the correct position.

**Time Complexity:** O(n + k) where n is the number of elements and k is the range of the input.

**When to Use:** Useful for sorting integers or objects that can be mapped to integers, especially when the range of numbers (k) is not significantly larger than the number of elements (n).

```c
void countingSort(int arr[], int n) {
    int output[n];
    int max = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > max)
            max = arr[i];
    }
    int count[max+1];
    for (int i = 0; i <= max; i++)
        count[i] = 0;
    for (int i = 0; i < n; i++)
        count[arr[i]]++;
    for (int i = 1; i <= max; i++)
        count[i] += count[i-1];
    for (int i = n-1; i >= 0; i--) {
        output[count[arr[i]]-1] = arr[i];
        count[arr[i]]--;
    }
    for (int i = 0; i < n; i++)
        arr[i] = output[i];
}
```

## 5. Quick Sort

**Unique Feature:** Divides the array into sub-arrays around a pivot and recursively sorts them.

**Time Complexity:** O(n log n) on average, O(n^2) in the worst case.

**When to Use:** Prefer it for large datasets due to its average-case performance and low memory usage.

```c
int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
    int temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;
    return (i + 1);
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```

## 6. Merge Sort

**Unique Feature:** Recursively splits the array into halves, sorts each half, and then merges them back together.

**Time Complexity:** O(n log n) in all cases.

**When to Use:** Prefer it for large datasets and when stable sorting is required.

```c
void merge(int arr[], int l, int m, int r) {
    int n1 = m - l + 1;
    int n2 = r - m;
    int L[n1], R[n2];
    for (int i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];
    int i = 0;
    int j = 0;
    int k = l;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);
        merge(arr, l, m, r);
    }
}
```
