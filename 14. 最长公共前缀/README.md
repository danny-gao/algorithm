# 14. 最长公共前缀
给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。
## Example
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

## solution
1.遍历string字符串，用第一个字符串与其他字符串判断公共前缀，保留公共前缀的最小值

``` 
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.size() == 0)
        {
            return "";
        }

        string comparestr = strs[0];
        int maxlenth = comparestr.size();
        int count = 0;
        for(int index=1; index<strs.size(); index++)
        {
            count = 0;
            for(int j=0; j < comparestr.size() && j < strs[index].size(); j++)
            {
                if(comparestr[j] == strs[index][j])
                {
                    count++;
                }
                else
                {
                    break;
                }
            }

            maxlenth = min(count, maxlenth);
        }
        return comparestr.substr(0, maxlenth);
    }
```
