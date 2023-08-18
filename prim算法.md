
#prim算法

注意最后输出答案，要先把prim的值赋给一个变量，再输出那个变量
然后要注意过程中有无使用两等号，如果有注意是否满足bool要求
prim算法的原理是，构造最小生成树的点集合，当点集合为满时结束过程。每一次选择到点集合距离最短的点进入，并将对应的边加上，生成新的树。<font color=red>每选择一次节点，需要更新一次每个点到集合的距离</font>。

模板：

```
# include<bits/stdc++.h>
# include<algorithm>
typedef long long ll;
int n,m;
int p[5100][5100];
int dis[5100];
bool istrue[5100];
using namespace std;
int prim()
{
	int res=0;
	memset(dis,0x3f,sizeof dis);      //在此注意要将dis距离初始化为无穷大
	for(int i=0;i<n;i++)
	{
		int t=-1;
		for(int j=1;j<=n;j++)
		{
			if(!istrue[j]&&(t==-1||dis[j]<dis[t]))
			t=j;
		}
		if(i&&dis[t]==0x3f3f3f3f)     //第一次的时候的距离必然为无限大，所以需要特判
		return 114514;
		if(i)
		res+=dis[t];
		istrue[t]=true;
		for(int j=1;j<=n;j++)
		dis[j]=min(dis[j],p[t][j]);
		
	}
	return res;
}

int main (void)
{
	cin>>n>>m;
	memset(p,0x3f,sizeof p);
	
	for(int i=0;i<m;i++)
	{
		int a,b,c;
		cin>>a>>b>>c;
		p[a][b]=p[b][a]=min(p[a][b],c);
	}
	int t=prim();
	if(t==114514)
	{
		cout<<"orz"<<endl;
		return 0;
	}
	cout<<t<<endl;
	return 0;
	
}
```
