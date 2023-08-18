bf算法用于求解单源最短路径问题。但是算法的复杂度在稠密图中偏高，接近o(V*E);

原理是迭代n次，每一次迭代遍历一遍所有的边，并依据每个边长更新起点到各节点的距离。

bellman_ford在某些情况下可以处理带有负权环的图的最短距离问题。一般带负权环的图求解最短距离问题可能无解，因为一个负环走一遍总权值就会减少一次，那么走无数次总权值可以变为负无穷。在bellman_ford问题中如果对要走的边数做出了限制，那么就可以求解最短路。

[853. 有边数限制的最短路 - AcWing题库](https://www.acwing.com/problem/content/855/)

```
# include<bits/stdc++.h>
using namespace std;
typedef long long ll;


int n,m;
struct Edge
{
	int a,b,c;
};
const int N=1000005;

Edge edge[N];
int k;
int dis[N];
int last[N];

void spellman_ford()
{
	memset(dis,0x3f,sizeof dis);
	dis[1]=0;
	
	for(int i=0;i<k;i++)      //迭代k次，意味着只走k条边
	{
		memcpy(last, dis, sizeof dis);    //做备份，确保下一次遍历时更新依据只能是上一次更新结果
		
		for(int j=0;j<m;j++)
		{
			int a=edge[j].a;
			int b=edge[j].b;
			int c=edge[j].c;
			dis[b]=min(dis[b],last[a]+c);   //更新距离
			
			
		}	
	}
	
	if(dis[n]>=0x3f3f3f3f/2)
	puts("impossible");
	else
	cout<<dis[n];
	
		
}
int main (void)
{
	cin>>n>>m>>k;
	for(int i=0;i<m;i++)
	{
		int a,b,c;
		cin>>a>>b>>c;
		edge[i]={a,b,c};
		
	}
	
	spellman_ford();
	
	
	return 0;
		
}
```