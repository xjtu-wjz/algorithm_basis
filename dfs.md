dfs本质就是一种递归算法，或者说可以后悔的搜索。

#全排列

对1~n的数字取出其中几个进行排列，输出排列方法。

[P1157 组合的输出 - 洛谷 | 计算机科学教育新生态 (luogu.com.cn)](https://www.luogu.com.cn/problem/P1157)

```
# include<bits/stdc++.h>
# include<iomanip>
using namespace std;
typedef long long ll;

ll n,r;
ll arr[22];
bool dis[22];

void dfs(int u)
{
	if(u==r)
	{
		for(int i=0;i<r;i++)
		cout<<setw(3)<<arr[i];
		cout<<endl;
		return ; 
	}
	
	if(u==0)
	{
		for(int i=1;i<=n;i++)
		{
			if(!dis[i])
			{
				arr[u]=i;
				dis[i]=true;
				dfs(u+1);
				dis[i]=false;
			}
		}
	}
	else
	{
	for(int i=arr[u-1];i<=n;i++)
	{
		if(!dis[i])
		{
			dis[i]=true;
			arr[u]=i;
			dfs(u+1);
			dis[i]=false;
		}
		
	
	}
	}
}
int main (void)
{
	cin>>n>>r;
	dfs(0);
	
	
	return 0;
		
}
```

#n皇后

n皇后问题本质上是带剪枝的dfs。

一种深搜方法：

[843. n-皇后问题 - AcWing题库](https://www.acwing.com/problem/content/845/)

```
# include<bits/stdc++.h>
using namespace std;
typedef long long ll;

int n;
char g[20][20];
bool col[20],dg[20],udg[20];

void dfs(int u)
{
	
	if(u==n)
	{
		for(int i=0;i<n;i++)
		{
			for(int j=0;j<n;j++)
			cout<<g[i][j];
			cout<<endl;
			
		}
		cout<<endl;
		return;
	}
	
	for(int i=0;i<n;i++)
	{
		if(!col[i]&&!dg[i+u]&&!udg[n-u+i])
		{
			g[u][i]='Q';
			col[i]=dg[i+u]=udg[n-u+i]=true;
			dfs(u+1);
			g[u][i]='.';
			col[i]=dg[i+u]=udg[n-u+i]=false;
			
		}
	}
}

int main (void)
{

	cin>>n;
	for(int i=0;i<n;i++)
	{
		for(int j=0;j<n;j++)
		g[i][j]='.';
			
	}
	dfs(0);
	
	return 0;
		
}
```


