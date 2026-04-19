3 forms

classic                         search in sorted array
rotated                         search in a sorted but rotated array
search on answer space          the array is not sorted, but the answer space is, you need t binary search on that


KEY INSIGHT:

Each iteration eliminates half the search space
Why lo <= hi: when lo == hi there's still one element to check — don't skip it
Why not (lo + hi) / 2: if both are near INT_MAX, addition overflows


Two things to burn into memory:

mid = lo + (hi - lo) / 2 — always. Overflow-safe.
Loop condition lo <= hi for exact match. lo < hi for left-boundary problems.


Binary Search — extended forms summary:

Classic          → sorted array, find value         → lo <= hi
Peak Element     → unsorted, follow slope gradient  → lo < hi
2D Matrix        → map 2D → 1D with mid/n, mid%n    → lo <= hi
Answer Space     → search over possible answers     → lo < hi
Median partition → search partition point           → lo <= hi

All share: mid = lo + (hi-lo)/2, eliminate half each step


Template

1. classic

int low = 0, high = n-1;

while( low <= high>)
{
    int mid = low + (high-low)/2;                      // avoid overflow, dont use    (low+high)/2;

    if(arr[mid] == target)
        return mid;

    if(arr[mid] < target>)
        low = mid+1;
    else
        high = mid-1;

}

return -1; //not found





2. rotated sorted array

int low=0, high=n-1;


while(low <= high>)
{
    int mid = low + (high-low)/2; //to avoid overflow if low and high are near to INT_MAX;

    if( arr[mid]== target ) return mid;

    if(arr[low] <= arr[mid])  //this means left part of array is sorted. search for the value there
    {
        //is target in the sorted left half?
        if(arr[low] <= target && target <= arr[mid])
            high = mid - 1;
        else
            low = mid + 1;
    }
    else // right part is thesorted array.
    {
        //Is target in the soretd right half?
        if(arr[mid] <= target && target <= arr[high]) 
            low = mid+1;
        else
            high = mid-1;

    }
}

return -1;



KEY INSIGHT:
At every step, at least one half is guaranteed to be sorted
Check if target falls within the sorted half — if yes search there, if no search the other
The condition nums[lo] <= nums[mid] identifies the sorted half (equal handles the single-element case)



3. Binary search on answer space

TRIGGER — use this pattern when you see:
  → "minimum X such that condition is met"
  → "maximum X such that condition is met"
  → "find the smallest/largest value that satisfies..."
  → The answer is a number with a clear min and max bound

STEPS:
  1. Define lo = minimum possible answer
  2. Define hi = maximum possible answer
  3. Write feasible(mid): returns true if mid is a valid answer
  4. If feasible(mid): hi = mid   (search left — try smaller)
     Else:            lo = mid+1  (search right — need larger)
  5. Return lo

COMPLEXITY: O(n log(answer_range))
  — n from the feasibility check
  — log(answer_range) from the binary search itself

CEILING DIVISION: (a + b - 1) / b  ← integer ceiling without float cast


























