# Java Data Structures and Algorithms Cheatsheet


#### ArrayList
A resizable array implementation.

```java
List<Integer> arrList = new ArrayList<>();
arrList.add(10);      // Add element
arrList.add(1, 20);   // Insert element at index
arrList.remove(1);    // Remove element at index
int num = arrList.get(0); // Access element
```
**Time Complexity**:

| Operation   | Time Complexity |
|-------------|-----------------|
| Access      | O(1)            |
| Insertion   | O(n)            |
| Deletion    | O(n)            |

**Keywords:** dynamic array, contiguous memory

**Best Use Cases:** Frequent access operations, dynamic sizing

**Pros:** Fast random access (O(1) for get operations), dynamic resizing

**Cons:** Slow insertion and deletion, except at the end (O(n))

---


#### LinkedList
A doubly linked list implementation.

```java
List<Integer> linkedList = new LinkedList<>();
linkedList.add(10);       // Add element
linkedList.addFirst(20);  // Add to the front
linkedList.removeLast();  // Remove last element
```

**Time Complexity**:

| Operation   | Time Complexity |
|-------------|-----------------|
| Access      | O(n)            |
| Insertion   | O(1)            |
| Deletion    | O(1)            |

**Keywords:** linked nodes, non-contiguous memory

**Best Use Cases:** Frequent insertions and deletions, queues, and stacks

**Pros:** Efficient insertions/deletions

**Cons:** Slow access time, high memory usage due to pointers

---

#### HashSet
An unordered collection with unique elements.

```java
Set<String> hashSet = new HashSet<>();
hashSet.add("apple");    // Add element
hashSet.contains("apple"); // Check existence
hashSet.remove("apple"); // Remove element
```

**Time Complexity**:

| Operation   | Time Complexity |
|-------------|-----------------|
| Access      | O(1)            |
| Insertion   | O(1)            |
| Deletion    | O(1)            |

**Keywords:** unique elements, hashing

**Best Use Cases:** Eliminating duplicates, fast lookups

**Pros:** Fast operations, unique elements

**Cons:** Unordered, no indexed access

---

#### TreeSet
A sorted collection of unique elements (uses Red-Black Tree).

```java
Set<Integer> treeSet = new TreeSet<>();
treeSet.add(10);        // Add element
treeSet.add(5);         // Insert element
treeSet.remove(5);      // Remove element
int first = treeSet.first(); // Access first element
```

**Time Complexity**:

| Operation   | Time Complexity |
|-------------|-----------------|
| Access      | O(log n)        |
| Insertion   | O(log n)        |
| Deletion    | O(log n)        |

**Keywords:** sorted set, balanced tree

**Best Use Cases:** Maintaining sorted order, range queries

**Pros:** Sorted, fast access to min/max

**Cons:** Slower than HashSet

---

#### PriorityQueue
A queue where elements are ordered by priority (natural order by default).

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.add(10);            // Add element
pq.add(5);             // Insert element
int min = pq.peek();   // Access top element
pq.poll();             // Remove top element
```

**Time Complexity**:

| Operation   | Time Complexity |
|-------------|-----------------|
| Access(peek)| O(1)            |
| Insertion   | O(log n)        |
| Deletion    | O(log n)        |

**Keywords:** priority queue, heap

**Best Use Cases:** Task scheduling, finding smallest/largest element

**Pros:** Automatic ordering, efficient for priority-based access

**Cons:** No random access, extra sorting overhead


---

#### HashMap
A collection of key-value pairs where keys are unique, backed by a hash table.

```java
Map<String, Integer> hashMap = new HashMap<>();
hashMap.put("apple", 10);   // Insert key-value pair
hashMap.get("apple");       // Get value by key
hashMap.remove("apple");    // Remove key-value pair
```

**Time Complexity**:

| Operation   | Time Complexity |
|-------------|-----------------|
| Access      | O(1)            |
| Insertion   | O(1)            |
| Deletion    | O(1)            |

**Keywords:** key-value, hashing

**Best Use Cases:** Fast lookups by key, dictionary-style access

**Pros:** Fast operations

**Cons:** No ordering, requires good hash function

---

#### TreeMap
A sorted map based on a Red-Black Tree.

```java
Map<String, Integer> treeMap = new TreeMap<>();
treeMap.put("apple", 10);   // Insert key-value pair
treeMap.get("apple");       // Get value by key
treeMap.remove("apple");    // Remove key-value pair
```

**Time Complexity**:

| Operation   | Time Complexity |
|-------------|-----------------|
| Access      | O(log n)        |
| Insertion   | O(log n)        |
| Deletion    | O(log n)        |

**Keywords:** sorted map, balanced tree

**Best Use Cases:** Maintaining sorted order of keys, range queries

**Pros:** Sorted keys, predictable order

**Cons:** Slower than HashMap

---

#### Sorting Algorithms

#### QuickSort
A divide-and-conquer algorithm that selects a pivot and partitions the array around it.

```java
public class QuickSort {
    // Function to partition the array
    int partition(int arr[], int low, int high) {
        int pivot = arr[high];
        int i = (low - 1); // Index of smaller element
        for (int j = low; j < high; j++) {
            if (arr[j] < pivot) {
                i++;
                // Swap arr[i] and arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
        // Swap arr[i + 1] and arr[high] (pivot)
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return i + 1;
    }

    // Function that implements QuickSort
    void sort(int arr[], int low, int high) {
        if (low < high) {
            int pi = partition(arr, low, high);
            sort(arr, low, pi - 1); // Recursively sort elements before partition
            sort(arr, pi + 1, high); // Recursively sort elements after partition
        }
    }

    public static void main(String args[]) {
        int arr[] = {10, 7, 8, 9, 1, 5};
        int n = arr.length;
        QuickSort qs = new QuickSort();
        qs.sort(arr, 0, n - 1);
        System.out.println("Sorted array:");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
    }
}
```

- **Time Complexity**:
  - Best Case: O(n log n)
  - Worst Case: O(n²)
- **Best Use Cases**: Large datasets, average-case fast performance
- **Pros**: Fast for average-case, in-place sorting
- **Cons**: Worst-case O(n²), unstable

#### MergeSort
A stable, divide-and-conquer algorithm that merges sorted subarrays.

```java
public class MergeSort {
    // Merge two subarrays of arr[]
    void merge(int arr[], int l, int m, int r) {
        int n1 = m - l + 1;
        int n2 = r - m;

        // Create temp arrays
        int L[] = new int[n1];
        int R[] = new int[n2];

        // Copy data to temp arrays
        for (int i = 0; i < n1; ++i)
            L[i] = arr[l + i];
        for (int j = 0; j < n2; ++j)
            R[j] = arr[m + 1 + j];

        // Merge the temp arrays
        int i = 0, j = 0;
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

        // Copy remaining elements of L[]
        while (i < n1) {
            arr[k] = L[i];
            i++;
            k++;
        }

        // Copy remaining elements of R[]
        while (j < n2) {
            arr[k] = R[j];
            j++;
            k++;
        }
    }

    // Function that implements MergeSort
    void sort(int arr[], int l, int r) {
        if (l < r) {
            int m = (l + r) / 2;
            sort(arr, l, m); // Sort first half
            sort(arr, m + 1, r); // Sort second half
            merge(arr, l, m, r); // Merge the sorted halves
        }
    }

    public static void main(String args[]) {
        int arr[] = {12, 11, 13, 5, 6, 7};
        int n = arr.length;
        MergeSort ms = new MergeSort();
        ms.sort(arr, 0, n - 1);
        System.out.println("Sorted array:");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
    }
}
```

- **Time Complexity**:
  - Best Case: O(n log n)
  - Worst Case: O(n log n)
- **Best Use Cases**: Large datasets, needing stable sorting
- **Pros**: Stable, predictable O(n log n)
- **Cons**: Extra memory usage, slower than QuickSort in practice

#### Binary Search
Search a sorted array by repeatedly dividing the search interval in half.

```java
public class BinarySearch {
    // Binary search function
    int binarySearch(int arr[], int x) {
        int l = 0, r = arr.length - 1;
        while (l <= r) {
            int m = l + (r - l) / 2;
            // Check if x is present at mid
            if (arr[m] == x)
                return m;
            // If x greater, ignore left half
            if (arr[m] < x)
                l = m + 1;
            // If x is smaller, ignore right half
            else
                r = m - 1;
        }
        // If the element is not present in array
        return -1;
    }

    public static void main(String args[]) {
        BinarySearch bs = new BinarySearch();
        int arr[] = {2, 3, 4, 10, 40};
        int x = 10;
        int result = bs.binarySearch(arr, x);
        if (result == -1)
            System.out.println("Element not present");
        else
            System.out.println("Element found at index " + result);
    }
}
```

- **Time Complexity**:
  - Best Case: O(1) – when the element is in the middle of the array on the first try.
  - Worst Case: O(log n) – when the element is located at one of the ends of the array or not present at all.
- **Best Use Cases**: Searching in sorted arrays
- **Pros**: Very fast for sorted data
- **Cons**: Only works on sorted arrays
- 
---
#### Documentation

[Java Documentation](https://docs.oracle.com/javase/8/docs/api/)
