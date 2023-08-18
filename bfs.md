宽度优先搜索可理解为从某一个点出发，一圈一圈的向外走。

#走迷宫

基本思想为从一个点出发，一圈一圈的往外搜索距离依次为0,1,2......的点，直到把终点纳入搜索范围内。如果终点距离没有被更新，则这个迷宫没有解。

[B3625 迷宫寻路 - 洛谷 | 计算机科学教育新生态 (luogu.com.cn)](https://www.luogu.com.cn/problem/B3625)

```
# include<bits/stdc++.h>
using namespace std;
typedef long long ll;
ll n,m;
char g[105][105];
ll d[105][105];
ll dx[4]={-1,1,0,0};
ll dy[4]={0,0,-1,1};

ll bfs()
{
	queue<pair<ll,ll>>q;
	memset(d,-1,sizeof d);
	
	d[0][0]=0;
	q.push({0,0});
	while(q.size())
	{
		auto now=q.front();
		q.pop();
		for(int i=0;i<4;i++)
		{
			for(int j=0;j<4;j++)
			{
				ll tempox=now.first+dx[i];
				ll tempoy=now.second+dy[i];
				
				if(g[tempox][tempoy]=='.'&&tempox>=0&&tempox<n&&tempoy>=0&&tempoy<m&&d[tempox][tempoy]==-1)
				{
					d[tempox][tempoy]=d[now.first][now.second]+1;
					q.push({tempox,tempoy});
					
				}
			}
		}
		
	}
	return d[n-1][m-1];
	
}
int main (void)
{
	cin>>n>>m;
	for(int i=0;i<n;i++)
	cin>>g[i];
	if(bfs()!=-1)
	cout<<"Yes"<<endl;
	else
	cout<<"No"<<endl;
	return 0;
	
}
```

#