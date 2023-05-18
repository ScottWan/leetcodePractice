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
