<h1>
  <span class="headline">Quick Sort in Java</span>
  <span class="subhead">Quick Sort</span>
</h1>

**Learning objective:** By the end of this lesson, you'll be able to explain a merge sort algorithm.

## Introduction to quick sort
Quick sort is a sorting algorithm that follows a divide-conquer-combine approach to sort data in linear data structures like arrays:

- **Divide** _(partition using pivot)_ : Pick a **pivot** element. Use the pivot element to create a partition in the array by rearranging its elements such that each element in the left partition (left of the pivot element) is less than or equal to the pivot element and each element in the right partition (right of the pivot element) is larger than the pivot element. Recursively, keep repeating this process until partitions contain only one element. 

- **Conquer**  _(combine partitions)_ : Combine the partitions by discarding the pivot. The recursion in the **Divide** steps ensures that the partitions are combined in a LIFO manner (The last partitions to be created are the first partitions to be combined).

## Pivot selection strategies
Picking a good pivot is necessary for the fast execution of quicksort algorithms. The more equal the size of the partitions, the more faster the algorithms. However, it is not practically efficient to predict the best pivot value for a dataset before a quicksort. Hence, a strategy to choose a pivot needs to be decided before implementing the algorithm. Some of the commonly used strategies are:

### 1. Random element as the pivot
In this strategy, the pivot is chosen randomly from the array.

#### Advantages:

- **Better average case performance**: Randomly choosing a pivot reduces the likelihood of consistently poor partitions and avoids worst-case performance for sorted or nearly sorted data.
- **Balanced partitions**: Random selection tends to distribute elements relatively evenly in partitions over multiple iterations.
#### Drawbacks:

- **Overhead of randomization**: Generating a random index increases overhead slightly.
- **Unpredictable performance**: While it reduces the worst-case chance, it's still possible to pick an unfavorable pivot.

### 2. Leftmost element as the pivot
The pivot is always the first element in the array or partition.

#### Advantages:

- **Simple to implement**: The pivot index is fixed, making the partitioning logic straightforward.
- **No overhead**: No need for additional computations to determine the pivot.
#### Drawbacks:

- **Worst case for sorted data**: If the array is already sorted or reverse sorted, the partitioning will be extremely unbalanced, resulting in O(n^2) time complexity.
- **Poor performance for large data sets**: Unbalanced partitions increase the recursion depth, reducing efficiency for large inputs.

### 3. Rightmost element as the pivot
The pivot is always the last element in the array or partition.

#### Advantages:

- **Simple to implement**: Easy to select the pivot without any additional computation.
- **Consistent index**: Pivot selection doesn't change with different data structures.

#### Drawbacks:

- **Worst case for sorted data**: Similar to the leftmost strategy, sorted or reverse-sorted data results in poor partitioning.
- **Recursive depth issues**: Highly unbalanced partitions can cause stack overflow for large data sets.

### 4. Element with the median value as the pivot
The pivot is selected as the median value of the array of all the element values.

#### Advantages:

- **Optimal partitioning**: The median typically results in the most balanced partitions, improving overall performance.
- **Avoids worst case scenarios**: Works well even for sorted or reverse-sorted data, maintaining O(n log n) performance in such cases.
- **Efficient for large datasets**: Balanced partitions reduce recursion depth and improve performance on large inputs.

#### Drawbacks:

- **Computational overhead**: Determining the median requires extra computation.
- **Implementation complexity**: Finding the exact median requires the data set to be sorted. Hence, unless readily provided, computing the median value in a dataset to perform quick sort can become a complex _chicken-or-egg-first_ problem.



## Pseudocode for quick sort
Assuming a high degree of randomization and indeterminate size of the data set, the safest pivot selection strategy is choosing the right most element for an ascending sort. The rationale is the high degree of performance predictability of this strategy and the lack of any overhead. Let's look at the pseudocode implementation of such a quick sort algorithm.

```plaintext
FUNCTION quickSort(array, leftIndex, rightIndex):
    IF leftIndex < rightIndex:
        SET pivotIndex = partition(array, leftIndex, rightIndex)
        CALL quickSort(array, leftIndex, pivotIndex - 1)
        CALL quickSort(array, pivotIndex + 1, rightIndex)

FUNCTION partition(array, leftIndex, rightIndex):
    SET pivot = array[rightIndex]
    SET i = leftIndex - 1
    FOR j FROM leftIndex TO rightIndex - 1:
        IF array[j] <= pivot:
            SET i += 1
            EXECUTE SWAP (array[i], array[j])
    EXECUTE SWAP (array[i + 1], array[rightIndex])
    RETURN i + 1
```
## Time complexity of quick sort
Quick sort's performance heavily depends on the choice of the pivot and the distribution of the array's elements. The time complexity varies based on the best, average, and worst-case scenarios:

### Best case:
- **Scenario**: The best case occurs when the pivot divides the array into two nearly equal parts at every recursive step.
- **Complexity**: (O(n log n))
- **Reason**: This ideal partitioning results in each level of recursion involving (O(n)) operations, with the depth of the recursion tree being (log n).

### Average case:
- **Scenario**: Typical for randomly ordered data where the partitions are reasonably balanced.
- **Complexity**: (O(n log n))
- **Reason**: Assumes that the splits do not vary significantly from one recursive call to another, maintaining balanced work across the recursive tree.

### Worst case:
- **Scenario**: Occurs when the pivot is the smallest or largest element in the array.
- **Complexity**: (O(n^2))
- **Reason**: Each level of recursion operates over nearly the entire array, with the depth of the recursion reaching (n), leading to significantly increased processing time due to highly unbalanced partitions.
## Space complexity of quick sort
QuickSort is a recursive algorithm, and its space complexity largely depends on the depth of the recursion stack used during its execution.

- **In-place sorting**: QuickSort is considered an in-place sorting algorithm, which means it doesn't require additional storage proportional to the element count. However, it does utilize space on the stack for recursive calls.
- **Worst case**: In the worst case scenario, where the pivot choices are consistently poor (usually the smallest or largest element), the depth of the recursion tree can reach (n). This results in QuickSort requiring (O(n)) space on the stack.
- **Best and average case**:
With better pivot choices, typically either optimal or good enough, the recursion depth generally remains around (log n). Consequently, the space complexity in these cases is reduced to (O(log n)).

## Advantages of quick sort
- On average, Quick Sort has a time complexity of O(n log n).
- Its in-place sorting technique requires minimal extra storage.
- It works well for various data distributions.

## Drawbacks of quick sort
- Its time complexity Degenerates to O(n^2) if the pivot is not chosen well.
- Deep recursion can lead to stack overflow for large datasets.
- Equal elements may not maintain their relative order. In sorting algorithms, this is called an unstable sort.
## Final reflections
- Quick sort is a powerful sorting algorithm for large datasets.
- Partitioning logic efficiently separates elements based on the pivot.
- Recursive calls divide the problem until partitions have only one element.
- Quick sort uses only in-place operations. No extra arrays required, making it memory efficient.
- Best and average case performances are optimal O(n log n).
- Careful pivot selection can mitigate the risk of worst-case scenarios.
