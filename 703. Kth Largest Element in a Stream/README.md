# 703. Kth Largest Element in a Stream

Design a class to find the kth largest element in a stream. Note that it is the kth largest element in the sorted order, not the kth distinct element.

Implement KthLargest class:

    KthLargest(int k, int[] nums) Initializes the object with the integer k and the stream of integers nums.
    int add(int val) Returns the element representing the kth largest element in the stream.

寻找第K大元素
	
## Example

Input
["KthLargest", "add", "add", "add", "add", "add"]
[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
Output
[null, 4, 5, 5, 8, 8]

Explanation
KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
kthLargest.add(3);   // return 4
kthLargest.add(5);   // return 5
kthLargest.add(10);  // return 5
kthLargest.add(9);   // return 8
kthLargest.add(4);   // return 8
 
 
Input: nums = [1], k = 1
Output: [1]

## solution

1.使用优先队列(默认是大顶,std::less<int>)，使用std::great<int>小顶。优先队列保持K个元素，且顶部元素是最小的，也就是保证整个数组中第K大的元素。

```
/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest* obj = new KthLargest(k, nums);
 * int param_1 = obj->add(val);
 */

class KthLargest {
private:
    std::priority_queue<int, std::vector<int>, std::greater<int> > arr;
    int m_count;
public:
    KthLargest(int k, vector<int>& nums) {
        m_count = k;
        for(int var:nums)
        {
            if(arr.size() < m_count)
            {
                arr.push(var);
            }
            else
            {
                if(arr.top()<var)
                {
                    arr.pop();
                    arr.push(var);
                }
            }
        }
    }
    
    int add(int val) {
        if(arr.size() < m_count)
            {
                arr.push(val);
            }
            else
            {
                if(arr.top()<val)
                {
                    arr.pop();
                    arr.push(val);
                }
            }
        return arr.top();
    }
};


```