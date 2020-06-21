---
layout: post
title: "1007Maximum Subsequence Sum"
categories: Algorithm DP C++
---

Question
---------
><font face="楷体">求最大连续子序列和，输出最大的和以及这个子序列的开始值和结束值。
>如果所有的数都小于0，那么认为最大的和为0，并且输出首尾元素</font>  

Sample Input
------------

><strong>10  
>-10 1 2 3 4 -5 -23 3 7 -21</strong> 

Sample Output
-------------
><strong>10 1 4</strong>  

<font face="仿宋">首先，要注意一点，当所有的数都为负数时，输出的首尾元素，是<strong>整个数组的首尾元素</strong>。
如果注意不到这一点，第四个监测点是通不过的。</font>  
<font face="仿宋">这道题用到的是<strong>动态规划</strong>，动态规划说到底就是一种把大问题逐步分为重叠的若干小问题进行解决的思想，推荐一个讲动态规划很好的<a href="https://www.zhihu.com/question/23995189/answer/613096905">博文</a>。</font>  
<font face="仿宋">这道题中的思想也是比较简单，从第二个数字开始对比，该数字作为整个子序列的结尾加上之前一个数字的最大子序列是不是比该数字要大，如果大的话，就将该数字结尾的最大子序列更新，求出每个数字结尾的最大子序列之后，再找出其中最大的一个子序列，按规定格式输出。</font>

AC代码
------
```C++
//2020.2.17
//author:ViViWilliam
//issue7
#include<iostream>
using namespace std;

int main(){
	int n,sum;
	cin>>n;
	int nums[n],dp[n],site[n];
	for(int i=0;i<n;i++){
		cin>>nums[i];
		dp[i] = nums[i];
		site[i] = nums[i];
	}
	//dp
	//找出最大值
	 for(int i=1;i<n;i++){
	 	int nowsum=dp[i];
	 	
	 		nowsum+=dp[i-1];
	 		if(nowsum>dp[i]){
	 			dp[i] = nowsum;
	 			site[i] = site[i-1];
			 }
	 }
	 int max=0;
	 for(int i=1;i<n;i++){
	 	if(dp[i]>dp[max]){
	 		max = i;
		 }
	 }
	 
	 if(dp[max]<0){
	 	dp[max] = 0;
		 cout<<"0 "<<nums[0]<<" "<<nums[n-1];	
	 }
	 else
	cout<<dp[max]<<" "<<site[max]<<" "<<nums[max];
	return 0；
} 
```
