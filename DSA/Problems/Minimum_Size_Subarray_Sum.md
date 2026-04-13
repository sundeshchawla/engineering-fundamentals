# Minimum Size Subarray Sum (LeetCode #209)

Date: 4 Apr 2026
Difficulty: Medium
Pattern: → Sliding Window (Variable Size)
Language: C++

## Approach
Expand window by moving r right, adding nums[r] to sum.
Once sum >= target, the window is valid — record its length,
then shrink from the left (l++) subtracting nums[l] from sum.
Keep shrinking as long as the window stays valid.
This finds the minimum length window that meets the target.

## Time: O(n)  |  Space: O(1)

## My solution
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int sum = 0;
        int l = 0, minLen = INT_MAX;
        for (int r = 0; r < nums.size(); r++) {
            sum += nums[r];
            while (sum >= target) {
                minLen = min(minLen, r - l + 1);
                sum -= nums[l];
                l++;
            }
        }
        return minLen == INT_MAX ? 0 : minLen;
    }
};

## Core insight
The key difference from Longest Substring No Repeating:
THAT problem maximises window size — shrink only to fix violation.
THIS problem minimises window size — shrink aggressively
as long as the condition is still satisfied.
Both use variable sliding window but the shrink trigger is opposite:
  Longest: shrink when window becomes INVALID
  Minimum: shrink when window is VALID (squeeze out the answer)

The while loop placement is the tell:
  while(invalid) → you are finding the longest valid window
  while(valid)   → you are finding the shortest valid window

## Edge cases to verify
- No valid subarray exists: [1, 2, 3], target = 100
  → sum never reaches target, minLen stays INT_MAX
  → returns 0. Correct.

- Entire array needed: [1, 2, 3], target = 6
  → r expands to end, sum = 6 >= 6, minLen = 3
  → shrink: sum = 5, l = 1. While exits.
  → returns 3. Correct.

- Single element satisfies: [4, 1, 2], target = 4
  → r=0: sum=4>=4, minLen=1, shrink: sum=0, l=1. 
  → returns 1. Correct.

- All elements equal target: [4, 4, 4], target = 4
  → every single element satisfies alone
  → returns 1. Correct.

## What tripped me
[fill this in]

## Comparison with Longest Substring No Repeating
Feature              | Longest Substring      | Min Size Subarray
---------------------|------------------------|------------------
Goal                 | Maximise window        | Minimise window
Shrink trigger       | Window is invalid      | Window is valid
Update answer        | Every step after shrink| Inside while (on shrink)
Left pointer moves   | Until valid again      | Until invalid again

## Follow-up questions to think about

1. Why must minLen be initialised to INT_MAX and not 0?
   (If no valid subarray exists we return 0. If initialised
   to 0, every window beats it and you return wrong answer.
   INT_MAX is the sentinel for "not found yet".)

2. Can this be solved in O(n log n)?
   (Yes — prefix sums + binary search. Build prefix[i] = sum of
   first i elements. For each l, binary search for smallest r
   where prefix[r] - prefix[l] >= target. O(n log n) total.
   Know this exists — interviewers ask if you know alternatives.)

3. Maximum Size Subarray Sum Equals K (LeetCode #325 — premium)
   (Now target is exact, not minimum. Sliding window breaks for
   negative numbers. Needs prefix sum + HashMap approach instead.
   Good lesson: sliding window only works when all values positive.)

4. Subarray Sum Equals K (LeetCode #560)
   (Array can have negatives. Sliding window completely breaks.
   Prefix sum + HashMap is the only clean solution.
   Pattern shift: know when to abandon sliding window.)

5. Your solution shrinks with a while loop — same amortised
   O(n) argument as before. Can you explain it?
   (l only moves right, never left. Total l movements ≤ n.
   Total operations across all iterations = O(2n) = O(n).)