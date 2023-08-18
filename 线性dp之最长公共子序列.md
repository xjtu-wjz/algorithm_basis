#原理

现给定字符串a与b，定义f(i,j)的意义为：一直到a[i]和一直到b[j]的最长公共子序列的长度。因此对于a和b新加入的每一个字符，有如下定义方法：

- 若a[i]与b[j]相同，则f(i,j)=max(f(i-1,j-1)+1,f(i,j))；

值得注意的是，只有当新加入的字符（a[i]与b[j]）相同时，新的f(i,j)才能在前者的基础上加一。

一共有四种状态：
- 0 1 ：即字符串a不取最后一位，而b取最后一位
- 1 0：a取最后一位，b不取最后一位
- 00 和11相同。

模板如下：

```
# include<bits/stdc++.h>
using namespace std;
typedef long long ll;
ll n,m;
char a[1005];
char b[1005];
ll f[1005][1005];

int main (void)
{
	
	cin.tie(0);
	cout.tie(0);
	cin>>n>>m;
	cin>>a+1>>b+1;
		
	for(int i=1;i<=n;i++)
	{
		for(int j=1;j<=m;j++)
		{
		f[i][j]=max(f[i-1][j],f[i][j-1]);
		if(a[i]==b[j])
		{
			f[i][j]=max(f[i][j],f[i-1][j-1]+1);
			
		}
	}
			}		
	cout<<f[n][m]<<endl;
	return 0;
	
 } 
```


