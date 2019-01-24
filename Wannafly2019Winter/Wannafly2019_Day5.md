# CCPC-Wannafly Winter Camp 2019 Day5

## A Cactus Draw

```c++
//Time: 2ms Memory: 3MB
#include <bits/stdc++.h>
using namespace std;
#define M 5010
int n, m, num[M], vis[M], xx[M], yy[M];
int head[M], nxt[M], tot, ver[M];
void add(int x, int y)
{
	nxt[++tot] = head[x];
	head[x] = tot;
	ver[tot] = y;
}
void dfs(int x, int dep)
{
	num[dep]++;
	xx[x] = dep, yy[x] = num[dep];
	vis[x] = 1;
	for(int i = head[x]; i; i=nxt[i])
	{
		int y = ver[i];
		if(vis[y]) continue;
		dfs(y, dep + 1);
	}
}
int main()
{
	scanf("%d%d", &n, &m);
	for(int i = 0; i < m; i++)
	{
		int u, v;
		scanf("%d%d", &u, &v);
		add(u, v);
		add(v, u);
	}
	dfs(1, 1);
	for(int i = 1; i <= n; i++)
        printf("%d %d\n", xx[i], yy[i]);
	return 0;
}
```

## B Diameter

## C Division

```c++
//Time: 259ms Memory: 4MB
#include <bits/stdc++.h>
using namespace std;
#define ll long long
int main()
{
	ll n, k, temp, res = 0;
	priority_queue<ll>q;
	scanf("%lld%lld", &n, &k);
	while(n--)
	{
		scanf("%lld", &temp);
		res += temp;
		q.push(temp);
	}
	while(!q.empty() && k--)
	{
		temp = q.top();
		q.pop();
		if(temp >> 1) q.push(temp >> 1);
		res -= (temp - (temp >> 1));
	}
	printf("%lld", res);
}
```

## D Doppelblock

## E Fast Kronecker Transform

## F Kropki

## G Least Common Multiple

## H Nested Tree

## I Sorting

## J Special Judge

