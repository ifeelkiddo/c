#include <stdio.h>

void findSecondLargest(int arr[], int n) {
    if (n < 2) {
        printf("Array must contain at least two elements.\n");
        return;
    }
    
    int largest = arr[0], secondLargest = -1;
    
    for (int i = 1; i < n; i++) {
        if (arr[i] > largest) {
            secondLargest = largest;
            largest = arr[i];
        } else if (arr[i] > secondLargest && arr[i] != largest) {
            secondLargest = arr[i];
        }
    }
    
    if (secondLargest == -1) {
        printf("No second largest element found.\n");
    } else {
        printf("The second largest element is: %d\n", secondLargest);
    }
}

int main() {
    int arr[] = {12, 35, 1, 10, 34, 1};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    findSecondLargest(arr, n);
    
    return 0;
}
