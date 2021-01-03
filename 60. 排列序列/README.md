# 60. 排列序列
给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

给出集合 [1,2,3,...,n]，其所有元素共有 n! 种排列。

按大小顺序列出所有排列情况，并一一标记，当 n = 3 时, 所有排列如下：

    "123"
    "132"
    "213"
    "231"
    "312"
    "321"

给定 n 和 k，返回第 k 个排列。

## Example
输入：n = 3, k = 3
输出："213"

## solution
1.先定当前数字的索引index= k/(n-1)!   首位值的每一个值都有(n-1)!种排列，故index= k/(n-1)!，得到首位值的索引
  再更新k值 = k%(n-1)!                首位值选定后，k值应该减去首位值选定后的排列数量 故 k= k%(n-1)!
  再更新n值 = n-1                     当n数组中，某一个值被选定后，该值应该被剔除，故n = n-1
                                      循环往复，当k=0时，退出
``` 
int getFac(int n)
{
	int ret = 1;
	while (n>0)
	{
		ret = ret * n;
		n--;
	}
	return ret;
}

string getPermutation(int n, int k) {
	k--;
	int index = 0;
	int fac = 0;
	string str = string("123456789").substr(0, n);
	string ret;
	while (k>0)
	{
		fac = getFac(n - 1);
		index = k / fac;
		ret = ret + str[index];
		str = str.replace(str.begin() + index, str.begin() + index+1, "");
		k = k % fac;
		n--;
	}
	return ret+ str;
}

```
2.使用algorithm库的next_permutation函数，自动排序。对应的还有pre_permutation函数
``` 
string getPermutationEx(int n, int k) {
	string str = string("123456789").substr(0, n);

	while (k>1)
	{
		next_permutation(str.begin(), str.end());
		k--;
	}
	
	return str;
}
```