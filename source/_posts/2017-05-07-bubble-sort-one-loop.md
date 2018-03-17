---
title: "单个循环实现冒泡排序"
tags:
  - 冒泡排序
categories: 算法
toc: false
comment: true
notag: false
date: 2017-05-07 16:22:11
thumbnail:
---

* 普通的冒泡排序

```c
void BubbleSort(int arr[], int n) {
    int i, j, t;
    for(i=0; i<n; i++) {
        for(j=i+1; j<n; j++) {
            if(arr[i]>arr[j]) {
                t=arr[i]; arr[i]=arr[j]; arr[j]=t;
            }
        }
    }
}
```

* 使用一层循环实现的冒泡排序

```c
// 用宏实现变量交换
#define Swap(a,b,c) ((c)=(a),(a)=(b),(b)=(c))

// 第一种
void BubbleSortOneLoop(int arr[], int n)
{
    int i = 0;
    int l = 0;
    while (i < n - 1) //i还是控制最外层
    {
        if (arr[l] > arr[l +1])
        {
            int temp = 0;
            Swap(arr[l], arr[l + 1], temp);
        }
        l++;
        if (l >=n - i-1) //只不过在特殊点的时候改变l和i
        {
            l = 0;
            i++;
        }
    }
}

// 第二种
void BubbleSortOneLoop(int arr[], int n)
{
    int i = 0;
    int l = 0;
    int temp;
    while (i<n*n-1) //大次数为n*n-1，%n实现下标循环
    {
        if (arr[l%n] > arr[l%n + 1] && l%n<n-1-(i/n)) //直接判断
        {
            temp = 0;
            Swap(arr[l%n], arr[l%n + 1], temp);
        }
        l++; i++;
    }
}
```

冒泡法时间复杂度为 `O(n^2)` ，这个是改不了的，不可能因为用一个循环实现，就变成了 `O(n)`。所以，并没有什么卵用，只是一种写代码的方式而已。。。