# Kadane's Algorithm

## Core idea
Scan once. At each position decide: is my running sum
worth extending, or has it become a liability (gone negative)?
If negative, discard it and start fresh from here.

## The reset rule
if (currSum < 0) currSum = 0;
This is the entire algorithm. Everything else is bookkeeping.

## Initialisation rule — important
maxSum = nums[0], NOT 0.
If you initialise maxSum to 0 and all elements are negative,
you return 0 which is wrong — there was no empty subarray taken.

## Template
int maxSum = nums[0];
int currSum = 0;
for (int n : nums) {
    currSum += n;
    maxSum = max(maxSum, currSum);
    if (currSum < 0) currSum = 0;
}
return maxSum;

## Difference from Greedy Track Running Min/Max
Greedy Min/Max: keep a global anchor across the whole array
                (minimum price never gets discarded)
Kadane's:       actively discard the past when it turns negative
                (no global anchor — history is thrown away)

## Problems using this pattern
- Maximum Subarray → classic Kadane
- Maximum Sum Circular Subarray → Kadane + invert for min subarray
- Maximum Product Subarray → modified Kadane tracking min and max