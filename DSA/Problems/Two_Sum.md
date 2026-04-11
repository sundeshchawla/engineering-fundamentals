Two-Sum

Date: 3 Apr 2026
Difficulty: Easy
Pattern: → Hashing
Language: C++

## Approach
use an unordered_map where key is arr[i] and value is i;

run 1 loop only
	
	take diff = target - arr[i];
	check if the unordered_map contains key diff i.e mp.contains(diff) 
		if yes return { index i, index of matched value}
		
	
	check if current value exists in ordered set
		if not, then add it. i.e mp[arr[i]] = i;
## My code

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> mp ;

        for(int i=0; i < nums.size(); i++){
            int diff = target - nums[i];

            if(mp.contains(diff)){
                return { {i, mp[diff]} };
            }

            if(!mp.contains(nums[i])){
                mp[nums[i]] = i;
            }
        }

        return { {0,0} };
    }
};

## Time: O(n)  |  Space: O(n)

## What tripped me
//[whatever you found non-obvious — even if nothing, write "clean first attempt"]



## Follow-up question to think about
What if the array is sorted? (→ Two Pointers instead, O(1) space)