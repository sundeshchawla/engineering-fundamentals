# Maximum Subarray Sum (LeetCode #53)

Date: 4 Apr 2026
Difficulty: Medium
Pattern: → Kadane's Algorithm
Language: C++

## Approach
Maintain currSum and maxSum.
At each element, add it to currSum.
If currSum beats maxSum, update maxSum.
If currSum drops below 0, reset to 0 — a negative prefix
can never help any future subarray, so discard it.

## Time: O(n)  |  Space: O(1)

## My solution
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int maxSum = nums[0];
        int currSum = 0;

        for (int n : nums) {
            currSum += n;
            if (currSum > maxSum)
                maxSum = currSum;
            if (currSum < 0)
                currSum = 0;
        }
        return maxSum;
    }
};

## Core insight
A subarray with a negative sum is a liability.
If carrying it forward only drags down future elements,
cut it — start fresh from the next element.
The key decision at each step is not "should I extend
the window" but "is my current running sum still worth keeping."

This is why it is NOT the same as Track Running Min/Max.
There you keep a global anchor (the minimum price seen so far).
Here you throw away the past entirely when it turns negative.

## Edge cases to verify
- All negative: [-3, -1, -2]
  → maxSum initialises to nums[0] = -3
  → currSum hits -3, updates maxSum to -3, resets to 0
  → currSum hits -1, updates maxSum to -1, resets to 0
  → returns -1. Correct — best single element wins.
  
- Single element: [5] → returns 5. Correct.

- Mix: [-2, 1, -3, 4, -1, 2, 1, -5, 4]
  → answer is 6 (subarray [4,-1,2,1])
  → trace through manually once in your head.

## What tripped me
[fill this in]

## Follow-up questions to think about

1. What if you need to return the actual subarray, not just the sum?
   (Track start, end, and tempStart indices.
   When you reset currSum to 0, update tempStart = i + 1.
   When you update maxSum, save tempStart as start and i as end.)

2. Maximum Product Subarray (LeetCode #152) — same idea?
   (No. Negative × negative = positive, so you must track
   both the running maximum AND minimum at every step.
   Kadane's breaks here — needs a modified version.)

3. What if the array can be rotated and you want the max subarray
   in the circular version? (LeetCode #918)
   (Answer = max of: normal Kadane result OR total_sum - min_subarray.
   The second case handles wrap-around.)

4. Can you solve this with Divide and Conquer?
   (Yes — split array in half, max subarray is either in left half,
   right half, or crosses the midpoint. O(n log n) but interviewers
   ask this to test if you know multiple approaches.)

5. How does this connect to Best Time to Buy Sell Stock?
   (Convert prices[] to a daily diff array: diff[i] = prices[i] - prices[i-1].
   Max subarray sum of diff[] = max profit. Same problem, different skin.)