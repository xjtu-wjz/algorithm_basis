### 注意，优化版的jk算法需用邻接表表示图，模拟链表见[[单链表]]
### 同时jk算法用到邻接表图的遍历方法[[树与图的深度优先遍历与存储]]


#dijkstra优化

[850. Dijkstra求最短路 II - AcWing题库](https://www.acwing.com/problem/content/852/)

jk算法中最慢的一步在于找到点集中到集合距离最短的一个点。因此可以用堆来优化查找速度。

原理和朴素版jk算法一样，但是使用邻接表存储稀疏图。

```
# include<bits/stdc++.h>
using namespace std;
int n,m;
const int N=150005;

int e[N],h[N],idx,w[N],ne[N];
typedef pair<int,int>PII;

bool st[N];
int dist[N];

void add(int a,int b,int c)
{
	e[idx]=b;
	ne[idx]=h[a];
	w[idx]=c;
	h[a]=idx++;
	
}

int dijkstra()
{
	
	memset(dist,0x3f,sizeof dist);
	dist[1] = 0;
    priority_queue<PII, vector<PII>, greater<PII>> heap;//将堆设置为小根堆
    heap.push({0, 1});  //将最初的点，编号为1，到起点距离为0 的点压入堆中。
    
	while(heap.size())
	{
		auto t=heap.top();     
		heap.pop();
		int ver=t.second;    //ver是heap堆顶点的编号
		int distance=t.first;//distance是顶点到起点的距离
		
		if(st[ver])
		continue;            //如果该点已经入集合，直接跳过
		st[ver]=true;
		for(int i=h[ver];i!=-1;i=ne[i])
		{
			int j=e[i];
			
			if(dist[j]>distance+w[i])
			{
				dist[j]=distance+w[i];
				
				heap.push({dist[j],j});
				
			}
		}
	}
			
	if(dist[n]==0x3f3f3f3f)
	return -1;
	else
	return dist[n];
	
}
int main (void)
{
	cin>>n>>m;
	memset(h,-1,sizeof h);
	
	while(m--)
	{
		int a,b,c;
		cin>>a>>b>>c;
		add(a,b,c);
		
		
	}
	int t=dijkstra();
	cout<<t<<endl;
	return 0;
	
}

```