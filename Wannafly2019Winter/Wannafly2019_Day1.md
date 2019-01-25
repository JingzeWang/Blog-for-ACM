# CCPC-Wannafly Winter Camp 2019 Day1
## A

### 题解:

分类讨论6种

最多只会横向穿过两次

## B

### 题解：

> div2版本

dp\[i]\[j]\[k]: i，j表示位置，k表示时间，dp每个位置对应时间的最大糖果数

```c++
//Time: 11ms Memory: 14MB
#include <bits/stdc++.h>
using namespace std;
int dp[10200][12][12], a[12][12], vis[10200][12][12], n, m, c, t[12][12], sx, sy, tx, ty; 
int tt = 0; 
int main()
{
	cin >> n >> m >> c;
	for(int i = 1; i <= n; i++)
		for(int j = 1; j <= m; j++)
			cin >> t[i][j];
	cin >> sx >> sy >> tx >> ty;
	vis[0][sx][sy] = 1;
	while(tt != -1) 
	{
		tt++;
		for(int i = 1; i <= n; i++)
			for(int j = 1; j <= m; j++)
			{
				if(vis[tt - 1][i][j]) {dp[tt][i][j] = dp[tt - 1][i][j]; vis[tt][i][j] = 1;} 
				if(vis[tt - 1][i - 1][j]) {dp[tt][i][j] = max(dp[tt - 1][i - 1][j], dp[tt][i][j]); vis[tt][i][j] = 1;} 
				if(vis[tt - 1][i][j - 1]) {dp[tt][i][j] = max(dp[tt - 1][i][j - 1], dp[tt][i][j]); vis[tt][i][j] = 1;} 
				if(vis[tt - 1][i + 1][j]) {dp[tt][i][j] = max(dp[tt - 1][i + 1][j], dp[tt][i][j]); vis[tt][i][j] = 1;}
				if(vis[tt - 1][i][j + 1]) {dp[tt][i][j] = max(dp[tt - 1][i][j + 1], dp[tt][i][j]); vis[tt][i][j] = 1;} 
				if(tt % t[i][j] == 0 && vis[tt][i][j]) dp[tt][i][j]++;
			}
		if(dp[tt][tx][ty] >= c)
		{
			cout << tt << endl;
			return 0; 
		} 
	} 
}
```
> div1版本

dp1~10的循环节2520

向上倍增，最后加一个dp反向dp

## C

### 题解：

n<=2一定可行

## D

### 题解：

没...听...懂...

## E

### 题解

3n+1猜想

树上dp

搜索：枚举关键节点（3条边的节点，8个），剩下的是链，dp

## F

### 题解：

每座山可以绕过去也可以降下来

那么对于每座山，如果其高度大于k+第一座山的高度，那么任意点到它的边权为距离+降低高度的费用

dijkstra或spfa即可

```c++
//Time: 468ms Memory: 16MB
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const int M = 1e6 + 10;
const long long int INF = 0x3f3f3f3f3f3f3f3f;
int n, m, vis[M];
ll k, h[M], dis[M], temp;
int head[M], nxt[M], ver[M], tot;
ll edge[M];
priority_queue< pair<ll, int> > pq;
void add(int x, int y, ll z)
{
    nxt[++tot] = head[x];
    head[x] = tot;
    ver[tot] = y;
    edge[tot] = z;
}
void dijkstra()
{
    for(int i = 1; i <= n; i++) dis[i]=INF;
    dis[1] = 0;
    pq.push(make_pair(0, 1));
    while(!pq.empty())
    {
        ll x = pq.top().second;
        pq.pop();
        if(vis[x]) continue;
        vis[x] = 1;
        for(int i = head[x]; i != -1; i = nxt[i])
        {
            int y = ver[i];
            ll z = edge[i];
            if(dis[y] > dis[x] + z)
            {
                dis[y] = dis[x] + z;
                pq.push(make_pair(-dis[y], y));
            }
        }
    }
}
int main()
{
    cin >> n >> m >> k;
    for(int i = 1; i <= n; ++i) cin >> h[i];
    k += h[1];
    memset(head, -1, sizeof(head));
    while(m--)
    {
        int u, v;
        ll w;
        cin >> u >> v >> w;
        if(h[v] >= k) add(u, v, w + (h[v] - k) * (h[v] - k));
        else add(u, v, w);
        if(h[u] >= k) add(v, u, w + (h[u] - k) * (h[u] - k));
        else add(v, u, w);
    }
    dijkstra();
    cout << dis[n];
    return 0;
}
```

## G

### 题解：

i枚举gcd质因子

枚举上下左，右边扫，树状数组/线段树

## H

### 题解：

区间dp 不能过n^5

从下往上枚举葱的高度，区间分割成子区间，从下往上合并，i，j，k，第i~j的区间，k刀

## I

### 题解：

d[i][j]前i个数中小于j的个数

f(i)表示最后一个数字是i的序列数

循环1~i，比i小的数有多少个

f(i) = f(1) + (f(i) + 1) * (中间有多少个数)

中间有多少个数 = d\[i-1]\[pi]-d\[j]\[pj]；

div1:线段树维护(f\[i] + 1) * (中间有多少个数) 的sumA和sumT

## J

### 题解：

先统计出每个居民的宝物数量，进行升序排序

枚举m，认为i是居民拥有的最多的礼物数，超过i的全买下，如果不是最大数量，买最便宜的来补充自己的宝物

div1:权值线段树

## K

### 题解：

bfs树，统计每一个有特殊边的点，看黑暗势力先到还是光明势力先到

