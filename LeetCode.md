# LeetCode 每日一题题解

- 删除排序数组中的重复项

> 给你一个 升序排列 的数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。元素的 相对顺序 应该保持 一致 。然后返回 nums 中唯一元素的个数

```C
int removeDuplicates(int* nums, int numsSize)
{
    if((numsSize == 0) || (nums == NULL))
        return 0;
    else
    {
        int left = 0;
        for(int right = 1; right<numsSize; ++right)
        {
            if (nums[left] != nums[right])
            {
               nums[++left] = nums[right];
            }
        }
        return ++left; //最后一个也需要统计上
    }
}
```

- 买卖股票的最佳时机

> 给你一个整数数组`prices`，其中`prices[i]`表示第`i`天的价格，在每一天，你可以决定是否购买或者出售股票，你在任何时候`最多`只能持有一只股票， 你也可以先购买，然后在同一天出售，计算返回你能获得的最大利润

```C
int maxProfit(int* prices, int pricesSize)
{
    int nTotal = 0;
    for (int i = 0; i<pricesSize; ++i)
    {
        nTotal += (max(prices[i+1] - prices[i], 0));
    }
    return nTotal;
}

//动态规划解法
int maxProfit(int[] prices, int pricesSize) 
{
    if (prices == null || pricesSize < 2)
        return 0;
    int[][] dp = new int[pricesSize][2];
    //初始条件
    dp[0][1] = -prices[0];
    dp[0][0] = 0;
    for (int i = 1; i < pricesSize; i++) 
    {
        //递推公式
        dp[i][0] = max(dp[i - 1][0], dp[i - 1][1] + prices[i]);
        dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] - prices[i]);
    }
    //最后一天肯定是手里没有股票的时候，利润才会最大，
    //只需要返回dp[length - 1][0]即可
    return dp[length - 1][0];
}
```

- 旋转数组

> 给定一个整数数组`nums`，将数组中的元素向右轮转`k`个位置，其中`k`是非负数

```C++
void reverse(int[] nums, int start, int end)
{
    while(start<end)
    {
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
    }
}
void rotate(int* nums, int numsSize, int k)
{
    k %= numsSize;
    reverse(nums, 0, numsSize-1);   // 全部翻转
    reverse(nums, 0, k-1);          // 翻转前面的k个
    reverse(nums, k, numsSize-1);   // 翻转后面的
}
```

- 判断是否存在重复元素

> 给你一个整数数组`nums`,如果任一值在数组中出现 至少两次,返回`true`；如果数组中每个元素互不相同，返回`false`

```C++
bool containsDuplicate(int* nums, int numsSize)
{
    int left = 0;
    for (int left = 0; left<nums-1; ++left)
    {
        for (int right = left+1; right<numsSize; ++right)
        {
            if(nums[left] == nums[right])
            {
                return true;
            }
        }
    }
    return false;
}

//HashTable
#include <unordered_set>
bool containsDuplicate(std::vector<int>& nums)
{
    unordered_set<int> hash_map;
    for (int x:nums)
    {
        if(hash_map.find(x) != hash_map.end())
        {
            return true;
        }
        hash_map.insert(x);
    }
    return false;
}
```

- 只出现一次的数字

> 给你一个 非空 整数数组 nums ，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。
你必须设计并实现线性时间复杂度的算法来解决此问题，且该算法只使用常量额外空间。

```C++
//异或运算：相同为0， 不同为1
int singleNumber(int *nums, int numsSize)
{
    int reduce = 0;
    for (int num:nums)
    {
        reduce ^= num;
    }
    return reduce;
}
```

- 数组加一

> 给定一个由 整数 组成的 非空 数组所表示的非负整数，在该数的基础上加一。\
> 最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。\
> 你可以假设除了整数 0 之外，这个整数不会以零开头。

```C++
vector<int> AddOne(vector<int> &digits)
{
    int nSize = digits.size();
    for (int i = nSize-1; i>=0; --i)
    {
        if(digits[i] != 9)
        {
            digits[i]++;
            return digits;
        }
        else
        {
            digits[i] = 0;
        }    
    }
    //如果都是9， 则需要添加一位1.
}
```

- 移动零

> 给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。
> 请注意 ，必须在不复制数组的情况下原地对数组进行操作

```C++
void moveZeroes(vector<int>& nums)
{
    int left = 0; 
    for(int right = 0; right < nums.size(); ++right)
    {
        if (nums[right] != 0)
        {
            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;
            left++;
        }
    }
}
```
