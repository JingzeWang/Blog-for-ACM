# CCPC-Wannafly Winter Camp 2019 Day1
## A

### 题解:

分类讨论6种

最多只会横向穿过两次

## B

### 题解：

dp\[i]\[j]\[k]

div1版本

dp1~10的循环节2520

向上倍增，最后加一个dp反向dp

(队友的大腿是真的粗

```c++
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
	while(tt! = -1) 
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

spfa

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

