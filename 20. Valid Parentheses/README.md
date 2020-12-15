# 20. Valid Parentheses

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

## Example
Input: s = "()[]{}"
Output: true

Input: s = "([)]"
Output: false

## solution
1.用stack结构，当遇到 ( [ { ，则push进入stack，否则pop掉stack中的元素.
  最后判断stack是否为空，如果为空，就说明是有效括号字符串，否则就不是.

```
    bool isValid(string s) {
        std::stack<char> array;
        
        for(auto var : s)
        {
            if(var == '(' || var == '{' || var == '[')
            {
                array.push(var);
            }
            else
            {
                if(array.size() == 0)
                {
                    return false;
                }
                if(array.top() == findParentheses(var))
                {
                    array.pop();
                }
                else
                {
                    return false;
                }
            }
        }
        
        return array.empty()?true:false;
    }
    
    char findParentheses(char value)
    {
        char chret = ']';
        switch(value)
        {
            case '(' : 
                chret = ')';
                break;
            case '{' : 
                chret = '}';
                break;
            case '[' : 
                chret = ']';
                break;
            case  ')':
                chret = '(';
                break;
            case  '}' :
                chret = '{';
                break;
            default:
                chret = '[';
                break;
                
        }
        return chret;
    }
```

2.如果是有效括号的字符串，那么三种括号的 左括号和右括号的位置是对应的。
  那么，在字符串中replace三种括号()、[]、{}为空，如果最后string是空，那么是有效的，否则就不是 