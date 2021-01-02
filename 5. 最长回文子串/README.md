# 5. 最长回文子串
给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。
## Example
输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。

## solution
1.遍历string字符串，在每一个字符的位置向左右两个方向扩展判断是否是回文。
  注意区分 奇数 和 偶数 个子串
  注意 判断回文后，用索引位置和返回的长度，求解子串起始位置
	
``` 
    string longestPalindrome(string s) {
        int lenth = s.size();
        if(lenth <= 1)
        {
            return s;
        }

        int begin;
        int max=0;
        int jsub;
        int osub;
        for(int i=0; i<lenth-1; i++)
        {
            osub = isVaildEx(s, i, i+1);
            jsub = isVaildEx(s, i, i); 

            jsub = osub > jsub ? osub : jsub;

            if(jsub > max)
            {
                max = jsub;
                begin = i - (max-1)/2;
            }           
        }

        return s.substr(begin, max);
    }

    int isVaildEx(string sub, int left, int right)
    {     
        while(left>=0 && right< sub.size())
        {
            if(sub[left] != sub[right])
            {
                break;
            }
            left--;
            right++;
        }
        return right-left-1;
    }
```
2.暴力求解。遍历string字符串，求解每一个子串是否是回文。（超时）
  注意：除了暴力硬性判断字符串是否是回文，还可以让字符串反转，判断是否与原字符串一样来判断
``` 
      string longestPalindrome(string s) {
        int lenth = s.size();
        if(lenth <= 1)
        {
            return s;
        }
        string sub;
        int max = 0;
        int left = 0;
        for(int i=0; i<lenth-1; i++)
        {
            for(int j=i+1; j<lenth; j++)
            {
                sub = s.substr(i, j-i+1);
                if(j-i+1 > max )
                {
                    if(isVaild(sub))
                    {
                        max = j-i+1;
                        left = i;
                    }
                }
            }
        }

        return max==0? s.substr(0, 1) :s.substr(left, max);
    }

    bool isVaild(string sub)
    {
        string tmp = sub;
		//反转字符串判断是否与反转前相同
        std::reverse(std::begin(sub), std::end(sub)); 
        if(tmp == sub)
        {
            return true;
        }
        return false;
    }
```  
  