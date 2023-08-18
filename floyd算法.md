最简单的枚举法，依次取出图中的两个点并遍历图中的所有点，如果加入第三点距离变短，则更新距离。

[854. Floyd求最短路 - AcWing题库](https://www.acwing.com/problem/content/856/)

```
# include<bits/stdc++.h>
# include<algorithm>
typedef long long ll;
const int inf=1e9;

using namespace std;
ll n,m,q;
ll p[2030][2030];
ll dis[2030];
void floyd()
{
	for(int k=1;k<=n;k++)
	for(int i=1;i<=n;i++)
	for(int j=1;j<=n;j++)
	p[i][j]=min(p[i][j],p[i][k]+p[k][j]);
	
}
int main (void)
{
	cin.tie(0);
	cout.tie(0);
	cin>>n>>m>>q;
	for(int i=1;i<=n;i++)
	for(int j=1;j<=n;j++)
	if(i==j)
	p[i][j]=0;
	else
	p[i][j]=inf;
	
	for(int i=0;i<m;i++)
	{
		ll a,b,c;
		cin>>a>>b>>c;
		p[a][b]=min(p[a][b],c);
		}	
	floyd();
	while(q--)
	{
		int a,b;
		cin>>a>>b;
		int t=p[a][b];
		if(p[a][b]>inf/2)
		cout<<"impossible"<<endl;
		else
		cout<<p[a][b]<<endl;
		
	}
	return 0;
	
	
}
```