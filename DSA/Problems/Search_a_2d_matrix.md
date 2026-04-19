COmpletely wothout any searh or help i solved this

logic:
    assign values from 1-n to all the values since they are arranged in increasing order.
    get length and breadth i.e dimensions of 2d array.
    with value of mid calculate the index i and j. simple binary search


class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int len = matrix.size();
        int breadth = matrix[0].size();

        int low=0;
        int high = (len*breadth)-1;
        int mid, i, j, curr;

        while(low<=high)
        {
            mid = low + (high-low)/2;

            i = mid/breadth;
            j = mid%breadth;

            curr = matrix[i][j]; 

            if( curr == target)
                return true;
            
            if(curr < target)
                low = mid+1;
            else
                high = mid-1;
        }

        return false;
    }
};



gpt optimised version (cleaner)

class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size();
        int n = matrix[0].size();

        int low = 0, high = m * n - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            int val = matrix[mid / n][mid % n];

            if (val == target)
                return true;
            else if (val < target)
                low = mid + 1;
            else
                high = mid - 1;
        }

        return false;
    }
};

