# Maximum sum Rectangle

Given a 2D matrix M of dimensions RxC. Find the maximum sum submatrix in it.

## Examples

### Example 1:

**Input:**
R = 4
C = 5
M = [[1,2,-1,-4,-20],
     [-8,-3,4,2,1],
     [3,8,10,1,3],
     [-4,-1,1,7,-6]]
**Output:** 29
**Explanation:** The matrix is as follows and the blue rectangle denotes the maximum sum rectangle.

### Example 2:

**Input:**
R = 2
C = 2
M = [[-1,-2],[-3,-4]]
**Output:** -1
**Explanation:** Taking only the first cell is the optimal choice.

## Your Task:
You don't need to read input or print anything. Your task is to complete the function `maximumSumRectangle()` which takes the number R, C, and the 2D matrix M as input parameters and returns the maximum sum submatrix.

## Expected Time Complexity: O(R*R*C)
## Expected Auxiliary Space: O(R*C)

## Constraints:
- 1 <= R,C <= 500
- -1000 <= M[i][j] <= 1000

## Solution:

```cpp
class Solution {
public:
    int solve(vector<int>& v) {
        int n = v.size();
        int s = v[0];
        int gs = v[0];
        for (int i = 1; i < n; i++) {
            s = max(v[i], v[i] + s);
            gs = max(gs, s);
        }
        return gs;
    }

    int maximumSumRectangle(int R, int C, vector<vector<int>>& M) {
        vector<int> sum(R);
        int maxSum = INT_MIN;
        for (int i = 0; i < C; i++) {
            fill(sum.begin(), sum.end(), 0); 
            for (int j = i; j < C; j++) {
                for (int r = 0; r < R; r++) {
                    sum[r] += M[r][j]; 
                }
                int getSum = solve(sum);
                maxSum = max(maxSum, getSum);
            }
        }
        return maxSum;
    }
};