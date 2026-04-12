# Best Time to Buy and Sell Stock (LeetCode #121)

Date: 3 Apr 2026
Difficulty: Easy
Pattern: → Greedy (Track Running Min/Max)
Language: C++

## Approach
Track the minimum price seen so far as you scan left to right.
At each step, calculate profit if you sold TODAY (current - minSoFar).
Update maxProfit if this is better. Never look back.

## Time: O(n)  |  Space: O(1)

## My Solution:
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int minPrice = INT_MAX;
        int maxProfit = 0;

        for(int i=0; i< prices.size(); i++){
            if(prices[i] < minPrice)
                minPrice = prices[i];
            
            else if( prices[i] - minPrice > maxProfit)
                maxProfit = prices[i] - minPrice; 
        }

        return maxProfit;
    }
};


## Core insight
You don't need to check every buy-sell pair (that would be O(n²)).
The best sell price for any given day is always paired with the
lowest price seen BEFORE that day — so just track it greedily.

## What tripped me
I thought i create strart and end pointers and keep them moving, but wasnt sure what sould be the move condition.
and what if buy pointer has moved ahead of a cheaper day to buy and sell pointer can make more profit if buy hadnt moved.
couldnt crack the moving logic. had to see the solution.

## Follow-up questions to think about

1. What if prices = [7,6,4,3,1] — all decreasing?
   (minPrice keeps updating, maxProfit stays 0. Returns 0. Correct — 
   best action is to not trade.)

2. Best Time to Buy and Sell Stock II (LeetCode #122) — you can 
   make MULTIPLE transactions. How does the approach change?
   (Hint: add up every upward slope. No need to track min anymore.)

3. Best Time to Buy and Sell Stock with Cooldown (#309) — after 
   selling you must wait 1 day. Same greedy? Or does it break?
   (Greedy breaks here → needs DP. Good inflection point to remember.)

4. What if you had to return the actual buy and sell dates, 
   not just the profit value?
   (Track the index of minPrice, and save buy/sell indices when 
   maxProfit updates.)

5. Can you solve this with Kadane's Algorithm on a difference array?
   (Convert prices to daily changes: diff[i] = prices[i] - prices[i-1].
   Then max subarray sum on diff[] = same answer. Two ways to see 
   the same problem.)