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

# 1480. 一维数组的动态和

```
      /*
      给你一个数组 nums 。数组「动态和」的计算公式为：runningSum[i] = sum(nums[0]…nums[i]) 。

      请返回 nums 的动态和。

      示例 1：

      输入：nums = [1,2,3,4]
      输出：[1,3,6,10]
      解释：动态和计算过程为 [1, 1+2, 1+2+3, 1+2+3+4] 。
      示例 2：

      输入：nums = [1,1,1,1,1]
      输出：[1,2,3,4,5]
      解释：动态和计算过程为 [1, 1+1, 1+1+1, 1+1+1+1, 1+1+1+1+1] 。
      示例 3：

      输入：nums = [3,1,2,10,1]
      输出：[3,4,6,16,17]
       

      提示：

      1 <= nums.length <= 1000
      -10^6 <= nums[i] <= 10^6
    */

      /**
       * @param {number[]} nums
       * @return {number[]}
       */
      /*
        nums 输出的第一个值不变，输出的第二个值等于第一个和第二个的值
        第三个值等于输出数组中第二个和第三个的值（相当于原数组前三个的和）
        以此类推，一直递增
      */
      var runningSum = function (nums) {
        // 是否需要原地修改 nums
        // 如果不能原地修改, 就需要额外的数组空间
        // const sum = [nums[0]]
        for (let i = 1, len = nums.length; i < len; i++) {
          // sum[i] = sum[i - 1] + nums[i]
          nums[i] += nums[i-1]
        }
        return nums;
      };

      console.log(runningSum((nums = [1, 2, 3, 4]))); // [1,3,6,10]
      console.log(runningSum((nums = [1, 1, 1, 1, 1]))); // [1,2,3,4,5]
```
