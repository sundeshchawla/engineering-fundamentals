class Solution {
public:
    int shipWithinDays(vector<int>& weights, int days) {
        int low = *max_element(weights.begin(), weights.end()), mid;
        int high = accumulate(weights.begin(), weights.end(),0);

        while(low<high)
        {
            mid = low + (high-low)/2;

            if(canShip(weights, days, mid))
            {
                high = mid;
            }

            else
            {
                low = mid+1;
            }
        }

        return low;
    }

    bool canShip(vector<int>& weights, int days, int capacity)
    {
        int currCapacity = 0, currDay=1;

        for(int weight : weights)
        {
            currCapacity+=weight;
            
            if(currCapacity > capacity)
            {
                    currDay++;
                    currCapacity = weight;
            }
        }

        return currDay <= days;
    }
};