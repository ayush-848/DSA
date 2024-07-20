# 169. Majority Element I

Given an array `nums` of size `n`, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

## Examples

### Example 1:

**Input:** nums = [3,2,3]  
**Output:** 3

### Example 2:

**Input:** nums = [2,2,1,1,1,2,2]  
**Output:** 2

## Constraints:

- `n == nums.length`
- `1 <= n <= 5 * 10^4`
- `-10^9 <= nums[i] <= 10^9`

## Follow-up:

Could you solve the problem in linear time and in O(1) space?


### Solution :

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int n=nums.size();
        if(n==0){
            return 0;
        }if(n==1){
            return nums[0];
        }
        int e=nums[0];
        int sum=0;
        for(int i=0;i<n;i++){
            if(sum==0){
                e=nums[i];
            }
            if(nums[i]==e){
                sum+=1;
            }else{
                sum-=1;
            }
        }return e;
    }
};
