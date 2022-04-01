![mergesort](https://user-images.githubusercontent.com/22162410/161200800-d4d1b4c2-9376-4ba6-99ab-379c8286bfab.jpeg)

```c++
#include <array>

using std::array;

// Sorts the array in place (& reference), that's why the function doesn't return anything.
template <typename T, size_t size>
void merge(array<T, size> &arr, int startIndex, int endIndex, int middleIndex) {
    int i = startIndex;
    int k = startIndex;
    int j = middleIndex + 1;

    array<T, size> combined;

    while (i <= middleIndex && j <= endIndex) {
        if (arr[i] < arr[j]) {
            combined[k] = arr[i];
            k++;
            i++;
        } else {
            combined[k] = arr[j];
            k++;
            j++;
        }
    }

    while (i <= middleIndex) {
        combined[k] = arr[i];
        k++;
        i++;
    }

    while (j <= endIndex) {
        combined[k] = arr[j];
        k++;
        j++;
    }

    for (i = startIndex; i < k; i++) {
        arr[i] = combined[i];
    }
}

// Split and merge sort the array, recursively.
template <typename T, size_t size>
void mergeSort(array<T, size>& arr, int startIndex, int endIndex) {
    if (startIndex < endIndex) {
        int middleIndex = (startIndex + endIndex) / 2;
        mergeSort(arr, startIndex, middleIndex);        // going to left subtree
        mergeSort(arr, middleIndex + 1, endIndex);      // going to right subtree

        merge(arr, startIndex, endIndex, middleIndex);
    }
}

template <typename T, size_t size>
void mergeSort(array<T, size>& arr) {
    mergeSort(arr, 0, size - 1);
}

int main() {
    array<int, 6> arrayToSort({9, 7, 8, 3, 2, 1});
    mergeSort(arrayToSort);

    return 0;
}
```
