spfa本质是利用堆优化的spellman_ford算法。在bf中，对所有边要迭代n次，但是并不是每一次迭代都可以更新一次边的权值。因此可用队列存储更新的边，再进行宽搜更新其他的边。

spfa大部分时候可以处理正权图和负权图，**但是出题人可能会吧复杂度卡至nm**。因此先交一发，如果被卡住了就换。

#spfa求最短路

同dijkstra，spfa用于处理单源最短路。两者代码也非常相似。

总体过程：
>1.存边，并开队列存储所有可以被更新距离的节点。
>2.从起点开始遍历其出边。如果有需要更新距离的节点，那么更新距离；同时如果这个被更新距离的节点没有入队，则入队；
>3.重复操作直到队列为空。

[851. spfa求最短路 - AcWing题库](https://www.acwing.com/problem/content/853/)

```
# include<bits/stdc++.h>
using namespace std;
typedef long long ll;
int n,m;
const int N=100005;
int e[N],ne[N],h[N],idx,w[N];
int dis[N];
bool st[N];

int spfa()
{
	
	memset(dis,0x3f,sizeof dis);
	
	queue<int>q;
	
	dis[1]=0;
	q.push(1);
	
	while(q.size())
	{
		int t=q.front();
		q.pop();
		st[t]=false;
		for(int i=h[t];i!=-1;i=ne[i])
		{
			int j=e[i];
			
			if(dis[j]>dis[t]+w[i])
			{
				dis[j]=dis[t]+w[i];
				if(!st[j])
			{
				q.push(j);
				st[j]=true;
			}
			}
			
		}
	}
	
	if(dis[n]>=0x3f3f3f3f/2)
	return -114514;
	return dis[n];
	
}
void add(int a,int b,int c)
{
	e[idx]=b;
	ne[idx]=h[a];
	w[idx]=c;
	h[a]=idx++;
}
int main (void)
{
	memset(h,-1,sizeof h);
	
	cin>>n>>m;
	while(m--)
	{
		int a,b,c;
		cin>>a>>b>>c;
		add(a,b,c);
		
	}
	if(spfa()==-114514)
	puts("impossible");
	else
	cout<<spfa()<<endl;
	
}

```

#spfa判断负环

