又名染色法，需要借助公理：<font color=red>一个图是二分图，当且仅当图中没有奇数环（证明见wiki，简单的反证）</font>。

coloration代码实现原理很简单，dfs模拟染色过程，原则上一个二分图只要一个点确定了颜色，那么所有点都确定了颜色。因此如果中间染色情况出现矛盾则说明这个图不是二分图，退出搜索。

>c算法的图使用邻接表存储，模拟链表见[[单链表]]

[860. 染色法判定二分图 - AcWing题库](https://www.acwing.com/problem/content/862/)

```
# include<bits/stdc++.h>
using namespace std;
typedef long long ll;
ll n,m;
ll h[100005],e[200005],ne[200005];
ll idx;

void add(ll a,ll b)
{
	e[idx]=b;
	ne[idx]=h[a];
	h[a]=idx++;
	
}
ll color[100005];//false表示还没染过色 

bool dfs(ll k,ll x)
{
	color[k]=x;
	
	for(int i=h[k];i!=-1;i=ne[i])
	{
		int j=e[i];
		if(!color[j])
		{
			if(!dfs(j,3-x)) return false; 
		}
		else 
		if(color[j]==color[k])
		return false;
	}
	return true;
}
int main (void)
{
	cin>>n>>m;
	memset(h,-1,sizeof h);
	
	
	while(m--)
	{
		ll a,b;
		cin>>a>>b;
		add(a,b);
		add(b,a);	
	}
	
	bool flag=true;
	for(int i=1;i<=n;i++)
	{
		if(!color[i])
		{ 
		if(!dfs(i,1))
		{
			flag=false;
			break;
		}
	}
	}
		if(flag)
		{
			cout<<"Yes"<<endl;
		}
		else
		cout<<"No"<<endl;
		
	return 0;
		
}

```
