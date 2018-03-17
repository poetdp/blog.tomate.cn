---
title: "算法练习：数字重组"
tags:
  - 算法
  - 数字
  - 重组
categories: 算法
toc: false
comment: true
notag: false
date: 2017-05-30 15:30:41
thumbnail: http://upload-images.jianshu.io/upload_images/4368698-1b6460749fe74898.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
---

##### Description

输入一个N位高精度的正整数，去掉其中任意K个数字后剩下的数字按原左右次序组成一个新的正整数。写算法对给定的N和K，寻找一种方案使得剩下的数字组成的新数最小。

##### Input

N、K以及一个N位高精度的正整数

##### Output

剩下的数字组成的最小新数

##### Sample Input

20 5
89382735464109218767

##### Sample Output

235464109218767

##### Source

```cpp
#include <iostream>
using namespace std;

char find_min(char *c, int left, int right, int &pmin) {
	char min;
	min=c[left]; pmin=left; left++;
	while(left<=right) {
		if(c[left]<min) { min=c[left]; pmin=left;}
		left++;
	}
	return min;
}

int main() {
	int n, k;
	cin >> n >> k;
	char *c = new char [n];
	int i, pmin=0, tag=-1;
	for(i=0; i<n; i++) {
		cin >> c[i];
	}
	for(i=1; i<=n-k; i++) {
		cout << find_min(c, tag+1, k+i-1, pmin);
		tag=pmin;
	}
	cout << endl;
	return 0;
}
```