# Maximum Subarray Sum

Given an integer array `nums`, find the subarray with the largest sum, and return its sum.

## Examples

### Example 1:

**Input:** `nums` = [-2,1,-3,4,-1,2,1,-5,4] </br>
**Output:** = 6 </br>
**Explanation:** The subarray [4,-1,2,1] has the largest sum 6.

### Example 2:

**Input:** `nums` = [1] </br>
**Output:** 1 </br>
**Explanation:** The subarray [1] has the largest sum 1.

### Example 3:

**Input:** `nums` = [5,4,-1,7,8] </br>
**Output:** 23 </br>
**Explanation:** The subarray [5,4,-1,7,8] has the largest sum 23.

## Constraints:

- 1 <= nums.length <= 10^5
- -10^4 <= nums[i] <= 10^4

## Solution:

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& a) {
        int n = a.size();
        int currSum = a[0];
        int globalSum = a[0];

        for(int i = 1; i < n; i++){
            currSum = max(a[i], currSum + a[i]);
            globalSum = max(currSum, globalSum);
        }
        return globalSum;
    }
};
