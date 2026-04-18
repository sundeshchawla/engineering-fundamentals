class Solution {
public:
    int search(vector<int>& nums, int target) {
        int high=nums.size()-1, low=0, mid;

        while(low<=high)
        {
            mid = low + (high-low)/2;

            //below vars are not neede dwe can do direct comparieson. but this help me achieve 100% fastest execution at leetcode.
            int midVal = nums[mid], lowVal = nums[low], highVal = nums[high];

            if(midVal==target) return mid;


            if(lowVal <= midVal)
            {
                if(lowVal <= target && target <= midVal)
                    high = mid-1;
                else
                    low = mid+1;

            }
            else
            {
                if(midVal <= target && target <= highVal)
                    low = mid+1;
                else
                    high = mid-1;
            }
        }

        return -1;
    }
};