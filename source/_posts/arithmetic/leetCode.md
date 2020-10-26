---
title: LeetCode
date: 2020-10-24 14:16:14
tags: LeetCode刷题
categories: LeetCode刷题
cover: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1603642371527&di=e62970424c556a1af55cec879e787503&imgtype=0&src=http%3A%2F%2Fpic2.zhimg.com%2Fv2-7f53d6e705908911ddde697e445deed9_180x120.jpg'
hide: true
---

# 1365. 有多少小于当前数字的数字

```
     /*
      给你一个数组 nums，对于其中每个元素 nums[i]，请你统计数组中比它小的所有数字的数目。

      换而言之，对于每个 nums[i] 你必须计算出有效的 j 的数量，其中 j 满足 j != i 且 nums[j] < nums[i] 。

      以数组形式返回答案。

       

      示例 1：

      输入：nums = [8,1,2,2,3]
      输出：[4,0,1,1,3]
      解释：
      对于 nums[0]=8 存在四个比它小的数字：（1，2，2 和 3）。
      对于 nums[1]=1 不存在比它小的数字。
      对于 nums[2]=2 存在一个比它小的数字：（1）。
      对于 nums[3]=2 存在一个比它小的数字：（1）。
      对于 nums[4]=3 存在三个比它小的数字：（1，2 和 2）。
      示例 2：

      输入：nums = [6,5,4,8]
      输出：[2,1,0,3]
      示例 3：

      输入：nums = [7,7,7,7]
      输出：[0,0,0,0]
       

      提示：

      2 <= nums.length <= 500
      0 <= nums[i] <= 100
    */

      /**
       * @param {number[]} nums
       * @return {number[]}
       */
      /*
        暴力解法
        复杂度分析：
          时间复杂度：O(N2)
          空间复杂度：O(1)
        解题思路：
          i和j同时扫描数组
          扫描同时，通过 count 计数，让 num[i] 去 和 nums[j] 作比较
          如果 nums[i] > nums[j]，count 递增
          最后将 count 值记录到 resArr，返回这个数组
      */
      var smallerNumbersThanCurrent = function (nums) {
        const resArr = [];
        const len = nums.length;
        for (let i = 0; i < len; i++) {
          let count = 0;
          for (let j = 0; j < len; ++j) {
            if (nums[i] > nums[j]) {
              count++;
            }
          }
          resArr[i] = count;
        }
        return resArr;
      };

      console.log(smallerNumbersThanCurrent([8, 1, 2, 2, 3])); // [4,0,1,1,3]
      console.log(smallerNumbersThanCurrent([7, 7, 7, 7])); // [0,0,0,0]
```
