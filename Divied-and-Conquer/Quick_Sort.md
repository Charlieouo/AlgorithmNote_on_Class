# 引用自湖南大学姜文君教授的PPT
## 仅供学习使用
![image](https://github.com/Charlieouo/AlgorithmNote_on_Class/blob/main/pic/20210511124727.png)
## /*参考数据结构p274(清华大学出版社，严蔚敏)*/﻿
``` cpp
void Qsort(int arr[], int low, int high){
    if (high <= low) return;
    int i = low;
    int j = high + 1;
    int key = arr[low];
    while (true)
    {
        /*从左向右找比key大的值*/
        while (arr[++i] < key)
        {
            if (i == high){
                break;
            }
        }
        /*从右向左找比key小的值*/
        while (arr[--j] > key)
        {
            if (j == low){
                break;
            }
        }
        if (i >= j) break;
        /*交换i,j对应的值*/
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    /*中枢值与j对应值交换，其实也可以和i对应的值交换，因为此时j = i*/
    int temp = arr[low];
    arr[low] = arr[j];
    arr[j] = temp;
    Qsort(arr, low, j - 1);
    Qsort(arr, j + 1, high);
}
 
```
