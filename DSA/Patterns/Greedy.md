## Sub-pattern: Track Running Min/Max

Core idea: scan once, maintain a running best value, 
update answer greedily at each step.

Problems:
- Best Time to Buy Sell Stock → track running minimum
- Trapping Rain Water (variant) → track running max from both sides
- Maximum Subarray (Kadane's) → track running sum, reset when negative