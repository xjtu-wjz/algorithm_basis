K算法非常简单，原理是将所有边按照边权重从小到大排序，如果这条边的两个端点不在同一个连通块中，则把他们合并并且把边加入生成树中。

会用到并查集[[[并查集]]]

[859. Kruskal算法求最小生成树 - AcWing题库](https://www.acwing.com/problem/content/861/)

```
# include<bits/stdc++.h>
using namespace std;
typedef long long ll;

int n,m;
struct Edge
{
	int a,b,c;
};
Edge edge[200005];
bool cmp(Edge x,Edge y)
{
	return x.c<y.c;
}
int p[100005];

int find(int x)
{
	if(p[x]!=x)
	p[x]=find(p[x]);
	return p[x];
	
}
int main (void)
{
	cin>>n>>m;
	
	for(int i=0;i<m;i++)
	{
		int a,b,c;
		cin>>a>>b>>c;
		edge[i].a=a;
		edge[i].b=b;
		edge[i].c=c;
		
	}
	for(int i=1;i<=n;i++)
	p[i]=i;
	sort(edge,edge+m,cmp);
	
	int ans=0;
	
	int cnt=0;
	for(int i=0;i<m;i++)
	{
		int a=edge[i].a;
		int b=edge[i].b;
		
		if(find(a)!=find(b))
		{
			ans+=edge[i].c;
			p[find(a)]=find(b);
			cnt++;
			if(cnt==n-1)
			break;	
		}	
	}
	
	if(cnt<n-1)
	{
		puts("impossible");
	}
	else
	cout<<ans<<endl;
	
	return  0;
		
}
```