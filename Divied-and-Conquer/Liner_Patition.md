# 引用自湖南大学姜文君教授的PPT
## 仅供学习使用
![image](https://github.com/Charlieouo/AlgorithmNote_on_Class/blob/main/pic/20210511121444.png)

## 下面给出一个具体例子
### Question: 设计一个算法，找出数组中最小的k个数。以任意顺序返回这k个数均可。 
``` c++
class Solution {
    int partition(vector<int>& nums, int l, int r)
    {
        int pivot = nums[r];
        int i = l - 1;
        for(int j = l; j < r; ++j)
        {
            if(nums[j] <= pivot)
            {
                swap(nums[++i], nums[j]);
            }
        }
        swap(nums[i+1], nums[r]);
        return i + 1;
    }

    int randomized_partition(vector<int>& nums, int l, int r)
    { 
        int i = rand() % (r - l + 1) + l;//随机数从左臂l到右臂r
        swap(nums[r], nums[i]);
        return partition(nums, l, r);
    }

    void randomized_selected(vector<int>& nums, int l, int r, int k)
    {
        if(l >= r) return;
        int pos = randomized_partition(nums, l, r);
        int num = pos - l + 1;//坑
        if (k == num)
        {
            return;
        }
        else 
        {//如果num小于k，就在其右侧再找k-num个，否则就在其左侧找k个
            num < k ? randomized_selected(nums, pos + 1, r, k - num):randomized_selected(nums, l, pos - 1, k);
        }
    }

public:
    vector<int> smallestK(vector<int>& arr, int k) {
        srand((unsigned int)time(0));
        randomized_selected(arr, 0, (int)arr.size() - 1, k);
        vector<int>vec;
        for(int i = 0; i < k; ++i)
        {
            vec.push_back(arr[i]);
        }
        return vec;
     
    }
};
```
