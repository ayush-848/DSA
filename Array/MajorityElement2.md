# 229. Majority Element II

Given an integer array `nums` of size `n`, find all elements that appear more than `⌊ n/3 ⌋` times.

## Examples

### Example 1:

**Input:** nums = [3,2,3]  
**Output:** [3]

### Example 2:

**Input:** nums = [1]  
**Output:** [1]

### Example 3:

**Input:** nums = [1,2]  
**Output:** [1,2]

## Constraints:

- 1 <= nums.length <= 5 * 10<sup>4</sup>
- -10<sup>9</sup> <= nums[i] <= 10<sup>9</sup>

## Follow up:

Could you solve the problem in linear time and in O(1) space?


### Solution :

```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        int n=nums.size();
        if(n==1){
            return {nums[0]};
        }
        
        int el1=0;
        int el2=INT_MIN;
        int c1=0,c2=0;
         for (int i : nums) {
            if (i == el1) {
                c1++;
            } else if (i == el2) {
                c2++;
            } else if (c1 == 0) {
                el1 = i;
                c1++;
            } else if (c2 == 0) {
                el2 = i;
                c2++;
            } else {
                c1--;
                c2--;
            }
        }
        
        c1 = c2 = 0;
        for (int i : nums) {
            if (i == el1) c1++;
            else if (i == el2) c2++;
        }

        vector<int> ans;
        if (c1 > n / 3) ans.push_back(el1);
        if (c2 > n / 3) ans.push_back(el2);

        return ans;
    }
};
