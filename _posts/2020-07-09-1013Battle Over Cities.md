---
layout: post
title: "1013Battle Over Cities"
categories: PAT C++ Graph
---

Question
--------
><font face="楷体">给出n个城市之间有相互连接的m条道路，当删除一个城市和其连接的道路的时候，问其他几个剩余的城市至少要添加多少个路线才能让它们重新变为连通图</font>

Sample Input
------------

><strong>3 2 3  
>1 2  
>1 3  
>1 2 3  
</strong>

Sample Output
-------------

><strong>1  
>0  
>0  
</strong>

<font face="fangsong">这道题用到的是图得深度优先遍历，当a个互相分立得连通分量变为连通图的时候，只需要添加a-1条路线，我这道题是参照了柳神的代码，对于每一个被占领的城市，标记该城市为已访问，在深度优先遍历的时候，对所有的未访问节点进行遍历，求能求到所有的连通分量的个数，<strong>要注意的就是，每次重新开始判断新数据之前，要把之前的visit数组重置</strong>，这里用到的是fill()<sup>[1]</sup>函数</font>

<font face="fangsong">再就是，这道题我用c++的输入输出有时候会在最后一个测试点报运行超时的错，但是用c语言的输入输出就不会。</font>

<font face="fangsong">离着PAT甲级考试只有十几天了，这几天得加快进度。</font>




AC代码:
------

```C++
#include <cstdio>
#include <algorithm>
using namespace std;
//图的深度优先遍历
//每个点找最短连通
int m,n,k;
int visit[1010];
int road[1010][1010] = {0};

//深度优先遍历
void dfs(int r){
	visit[r]=1;
	for(int i=1;i<=m;i++){
		if(road[i][r]==1&&visit[i]!=1){
			dfs(i);
		}
	}
}



int main(){

	scanf("%d%d%d", &m, &n, &k);
	int road1,road2;
	for(int i=0;i<n;i++){
		scanf("%d%d", &road1, &road2);
		road[road1][road2] = road[road2][road1] = 1;
	}
	int occupied;
	for(int i=0;i<k;i++){
		fill(visit, visit + 1010, 0);
		scanf("%d", &occupied);
		int repair = 0;
		visit[occupied] = 1;
		for(int i=1;i<m+1;i++){
			if(visit[i]==0){
				dfs(i);
				repair++;
			}
		}
		printf("%d\n", repair - 1);
		//visit[occupied] = 0;
	}
	return 0;
}
```
[1] fill(arr, arr + n, 要填入的内容)
