# 1.two sum

## Example
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].

## solution
1.双for循环，第一层遍历所有元素a，第二层编译 该元素之后的元素b，用A+B判断


2.用unordered_map<数值，索引>（散列表），判断target与数之差是是否存在于map中
```
    vector<int> twoSum(vector<int>& nums, int target) 
	{
        std::unordered_map<int, int> arr;
        
        for(int index=0; index<nums.size(); index++)
        {
            if(arr.find(target-nums[index]) != arr.end())
            {
                return vector<int>{index, arr[target-nums[index]]};
            }
            
            arr[nums[index]] = index;
        }
        return vector<int>{};
    }
