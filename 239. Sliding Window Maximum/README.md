# 239. Sliding Window Maximum

You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

## Example

Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation: 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
 
 
Input: nums = [1], k = 1
Output: [1]

## solution

1.使用双向队列 deque，存储数组的索引。
	每次加入新元素的索引前，如果新元素大于队列尾部的元素，则队列剔除队尾元素，直至队尾元素大于新元素。然后添加新元素进入队列。即 保证队列头部的元素是整个窗口中最大的。
	判断队列头部的索引值与当前数组元素的索引值之差是否大于windows大小，如果大于，就剔除队列头部元素，直至满足windows大小限定。

```
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    vector <int> ans;
	int n = nums.size();
	deque<int> window;
	for (int index = 0; index < n; index++)
	{
		while (!window.empty())
		{
			if (nums[index] > nums[window.back()])
			{
				window.pop_back();
			}
			else
			{
				break;
			}
		}
		while (!window.empty())
		{
			if (index-window.front() >= k)
			{
				window.pop_front();
			}
			else
			{
				break;
			}
		}
		window.push_back(index);

		if (index >= k-1)
		{
			ans.push_back(nums[window.front()]);
		}
	}
	return ans;
}
```