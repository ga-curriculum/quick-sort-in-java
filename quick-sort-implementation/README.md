<h1>
  <span class="headline">Quick Sort in Java</span>
  <span class="subhead">Quick Sort Implementation</span>
</h1>

**Learning objective:** By the end of this lesson, you'll be able to code a quick sort algorithm in Java.

## Quick sort demo
```java
public class QuickSort {

    // Quick Sort function
    public static void quickSort(int[] array, int leftIndex, int rightIndex) {
        if (leftIndex < rightIndex) {
            // Partition the array
            int pivotIndex = partition(array, leftIndex, rightIndex);

            // Recursively sort elements before and after partition
            quickSort(array, leftIndex, pivotIndex - 1);
            quickSort(array, pivotIndex + 1, rightIndex);
        }
    }

    // Partition function
    private static int partition(int[] array, int leftIndex, int rightIndex) {
        int pivot = array[rightIndex]; // Pivot element
        int i = leftIndex - 1; // Pointer for smaller element

        for (int j = leftIndex; j < rightIndex; j++) {
            if (array[j] <= pivot) {
                i++;
                swap(array, i, j);
            }
        }

        swap(array, i + 1, rightIndex); // Place pivot in the correct position
        return i + 1;
    }

    // Swap function
    private static void swap(int[] array, int i, int j) {
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }

    // Driver code
    public static void main(String[] args) {
        int[] prices = {30, 10, 50, 20, 60, 40};

        System.out.println("Original Array:");
        for (int price : prices) {
            System.out.print(price + " ");
        }

        quickSort(prices, 0, prices.length - 1);

        System.out.println("\n\nSorted Array:");
        for (int price : prices) {
            System.out.print(price + " ");
        }
    }
}
```

