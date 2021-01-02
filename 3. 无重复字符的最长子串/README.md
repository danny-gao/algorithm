# 3. 无重复字符的最长子串
给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。
## Example
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

## solution
1.遍历string字符串，把每一个元素添加到set中。如果添加之前发现set中存在，则删除set中的元素。
  这里需要注意用一个left标签记录，用于删除set中的元素，而不是只删除重复的元素。
``` 
      int lengthOfLongestSubstring(string s) {
        std::set<char> arr;
        int lenth = 0;
        int left = 0;
        int size =0;
        for(int index=0; index<s.size(); index++)
        {
            while(arr.find(s[index]) != arr.end())
            {
                arr.erase(s[left++]);
            }
            arr.insert(s[index]);

            size = arr.size();
            lenth = max(lenth, size);
        }

        return lenth;
    }
```