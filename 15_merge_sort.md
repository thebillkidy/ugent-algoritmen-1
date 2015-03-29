# 5. Merge Sort
Merge Sort is a comparison algorithm that tries to sort the dataset by a **Divide And Conquer** method. The performance of this algorithm is O(n log n).

## 5.1. How

We start by splitting the array up into separate elements, then we start by merging pairs together and we make sure that the smallest element is always on the left (this makes sure that our first index on the end is correct too). If the array start getting bigger then 2 elements, then we join those larger arrays by going through their elements one by one and putting the smallest one first.

![enter image description here](https://lh5.googleusercontent.com/-lIq0bLrtHrU/VQWdT-Ncq3I/AAAAAAAAKjU/P4TQ0-766wY/s0/300px-Merge_sort_algorithm_diagram.png "300px-Merge_sort_algorithm_diagram.png")

For the implementation check paragraph `§5.4`.

## 5.2. Advantages and Disadvantages

**Advantages**
- Stable
- $\Theta(n*lg(n))$ Performance
- Doesn't need random access to data

**Disadvantages**
- Not adaptive
- $\Theta(n)$ extra space normal
- $\Theta(lg(n))$ Extra space for LinkedLists

## 5.3. Performance
|Worst Case|Average Case|Best Case|
|-|-|-|
|O(n log n)|O(n log n)|O(n log n)|

## 5.4. Implementation
Implementing this algorithm is not so hard if you know how to, you need to keep 2 methods in mind:
- Merge (Combines 2 arrays with each other)
- MergeSort (Main method, accepts a dataset, splits it and calls this method for those 2 splitted parts)

Then just recursively call MergeSort and you are done.

### 5.4.1 C++ Code

	void merge(vector<T> &v, const vector<T> &left, const vector<T> &right) const {
		// We will save our merged array here
        vector<T> result;
        
        // Create indexes for the 2 arrays
        int idxLeft = 0;
        int idxRight = 0;
        
        // Make sure we are not at the end of one of the arrays, else we can't compare
        while (idxLeft < left.size() && idxRight < right.size()) {
            if (left[idxLeft] < right[idxRight]) {
                result.push_back(left[idxLeft]);
                idxLeft++;
            } else {
                result.push_back(right[idxRight]);
                idxRight++;
            }
        }
        
        // Add remaining elements
        while (idxLeft < left.size()) {
            result.push_back(left[idxLeft]);
            idxLeft++;
        }
        
        while (idxRight < right.size()) {
            result.push_back(right[idxRight]);
            idxRight++;
        }
        
        // Set our vector on the result
        v = result;
    };
    
    void merge_sort(vector<T> &v) const {
        // Stop running recursively once we have 1 element!
        if (v.size() == 1) {
            return;
        }
        
        // Find the middle element
        vector<int>::iterator middle = v.begin() + (v.size() / 2);
        
        // Create our 2 sub arrays
        vector<T> left(v.begin(), middle);
        vector<T> right(middle, v.end());
        
        // Recursively call MergeSort again, needed for the left and right
        merge_sort(left);
        merge_sort(right);
        
        // Merge the left and the right array
        merge(v, left, right);
    }

## 5.5. Benchmark
|&nbsp;| 100 | 1.000 | 10.000 | 100.000 | 1.000.000
|-|-|-|-|-|-|
|Random Elements|0.000163|0.001637|0.018098|0.19313|2.01314
|Ascending Elements|0.000145|0.001474|0.016712|0.172718|1.85952
|Descending Elements|0.00015|0.001472|0.016825|0.173975|1.84874

## 5.6. Conclusion
When sorting a Linked List Mergesort is the best choice, however for normal arrays it is better to use other algorithms such as heap sort (which requires less space) or quicksort.