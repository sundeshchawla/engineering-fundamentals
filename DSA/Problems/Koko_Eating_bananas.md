class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int h) {
        int low = 1, mid;
        int high = *max_element(piles.begin(), piles.end());


        while(low < high)
        {
            mid = low + (high-low)/2;

            if(canEat(piles,h,mid))
                high=mid;
            
            else
                low=mid+1;
        }

        return low;
    }

    bool canEat(vector<int>& piles, int h, int cap)
    {
        int hours = 0;

        for(auto pile : piles){
            hours += (pile+cap-1)/cap; 
        }

        return hours <= h;
    }
};