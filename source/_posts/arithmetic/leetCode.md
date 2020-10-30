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

# 二叉树的前序遍历

```
      /*
      给定一个二叉树，返回它的 前序 遍历。

       示例:

        输入: [1,null,2,3]
          1
            \
            2
            /
          3

        输出: [1,2,3]
        进阶: 递归算法很简单，你可以通过迭代算法完成吗？
    */

      /**
       * Definition for a binary tree node.
       * function TreeNode(val, left, right) {
       *     this.val = (val===undefined ? 0 : val)
       *     this.left = (left===undefined ? null : left)
       *     this.right = (right===undefined ? null : right)
       * }
       */
      /**
       * @param {TreeNode} root
       * @return {number[]}
       */
      // 前序遍历：对于二叉树中的任意一个节点，先打印该节点，然后是左子树，然后是右子树
      // 中序遍历：对于二叉树中的任意一个节点，先打印左子树，然后是该节点，然后是右子树
      // 后序遍历：对于二叉树中的任意一个节点，先打印左子树，然后是右子树，然后是该节点

      // 前序遍历
      // var preorderTraversal = function (root) {
      //   const resultArr = [];
      //   const TreeNode = (root) => {
      //     if (root) {
      //       resultArr.push(root.val);
      //       TreeNode(root.left);
      //       TreeNode(root.right);
      //     }
      //   };
      //   TreeNode(root);
      //   return resultArr;
      // };

      // 迭代实现
      var preorderTraversal = function (root) {
        const resultArr = [];
        const stack = [];
        // 先让根节点入栈
        if (root) stack.push(root);
        while (stack.length > 0) {
          const currentTree = stack.pop();
          // 首先根节点出栈
          if (currentTree) resultArr.push(currentTree.val);
          // 因为栈是先入后出，所以先操作右子树，再操作左子树
          if (currentTree && currentTree.right) {
            stack.push(currentTree.right);
          }
          if (currentTree && currentTree.left) {
            stack.push(currentTree.left);
          }
        }
        return resultArr;
      };
      console.log(preorderTraversal([1, null, 2, 3])); // [1,2,3]
```

# 剑指 Offer 58 - II. 左旋转字符串

```
      /*
      字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

      示例 1：

      输入: s = "abcdefg", k = 2
      输出: "cdefgab"
      示例 2：

      输入: s = "lrloseumgh", k = 6
      输出: "umghlrlose"
             [0,0,0,0,0,0]

      限制：

      1 <= k < s.length <= 10000
    */
      /**
       * @param {string} s
       * @param {number} n
       * @return {string}
       */

      // var reverseLeftWords = function (s, n) {
      //   return s.slice(n) + s.slice(0, n);
      // };

      // 双指针
      /*
        解题思路：
        定义一个数组，数组内部初始值为 s.length - n 的个数，即不需要旋转的个数
        然后定义 i 和 j 指针，j 指针负责扫描整个数组
        如果当前索引小于 n，表示需要旋转的值，添加到 arr 数组
        如果索引大于等于 n，表示是不需要旋转的值，直接往数组填充，每次填充 i 都递增
      */
      var reverseLeftWords = function (s, n) {
        const arr = new Array(s.length - n);
        let i = 0,
          j = 0;
        while (j < s.length) {
          if (j < n) {
            arr.push(s[j]);
          } else {
            arr[i++] = s[j];
          }
          j++;
        }
        return arr.join('');
      };

      console.log(reverseLeftWords((s = 'abcdefg'), (k = 2))); // "cdefgab"
      console.log(reverseLeftWords((s = 'lrloseumgh'), (k = 6))); // "umghlrlose"
```

# 1207. 独一无二的出现次数

```
/*
      给你一个整数数组 arr，请你帮忙统计数组中每个数的出现次数。

      如果每个数的出现次数都是独一无二的，就返回 true；否则返回 false。

       

      示例 1：

      输入：arr = [1,2,2,1,1,3]
      输出：true
      解释：在该数组中，1 出现了 3 次，2 出现了 2 次，3 只出现了 1 次。没有两个数的出现次数相同。
      示例 2：

      输入：arr = [1,2]
      输出：false
      示例 3：

      输入：arr = [-3,0,1,-3,1,1,1,-3,10,0]
      输出：true
       

      提示：

      1 <= arr.length <= 1000
      -1000 <= arr[i] <= 1000
      */

      /**
       * @param {number[]} arr
       * @return {boolean}
       */
      /*
        定义一个对象 o1，循环 arr，将数值为该对象的键，出现的次数为值，
        对象 o2 用来做 做比较值的对象
        flag 默认为 true，没有两个数的出现次数相同
        循环 o1 判断，o1 的值是否存在 o2，不存在即为 改变值为 true，存在即为 false，同时改变返回值 flag 为 false
      */
      var uniqueOccurrences = function (arr) {
        let o1 = {}
            o2 = {},
            flag = true

        for(let i = 0; i < arr.length;i++){
          if(!o1[arr[i]]) {
            o1[arr[i]] = 1
          } else {
            o1[arr[i]] = o1[arr[i]] + 1
          }
        }

        for(let key in o1) {
          if(!o2[o1[key]]) {
            o2[o1[key]] = true
          } else {
            flag = false
            o2[o1[key]] = false
          }
        }
        return flag
      };

      console.log(uniqueOccurrences((arr = [1, 2, 2, 1, 1, 3]))); // true
      console.log(uniqueOccurrences((arr = [1, 2]))); // false
      console.log(uniqueOccurrences((arr = [-3, 0, 1, -3, 1, 1, 1, -3, 10, 0]))); // true
      console.log(uniqueOccurrences((arr = [3, 5, -2, -3, -6, -6]))); // false
```

# 129. 求根到叶子节点数字之和

```
      /*
      给定一个二叉树，它的每个结点都存放一个 0-9 的数字，每条从根到叶子节点的路径都代表一个数字。

      例如，从根到叶子节点路径 1->2->3 代表数字 123。

      计算从根到叶子节点生成的所有数字之和。

      说明: 叶子节点是指没有子节点的节点。

      示例 1:

      输入: [1,2,3]
          1
        / \
        2   3
      输出: 25
      解释:
      从根到叶子节点路径 1->2 代表数字 12.
      从根到叶子节点路径 1->3 代表数字 13.
      因此，数字总和 = 12 + 13 = 25.
      示例 2:

      输入: [4,9,0,5,1]
          4
        / \
        9   0
       / \
      5   1
      输出: 1026
      解释:
      从根到叶子节点路径 4->9->5 代表数字 495.
      从根到叶子节点路径 4->9->1 代表数字 491.
      从根到叶子节点路径 4->0 代表数字 40.
      因此，数字总和 = 495 + 491 + 40 = 1026.
      */

      /**
       * Definition for a binary tree node.
       * function TreeNode(val) {
       *     this.val = val;
       *     this.left = this.right = null;
       * }
       */
      /**
       * @param {TreeNode} root
       * @return {number}
       */
      /*
        深度优先搜索
        复杂度分析:
            时间复杂度：O(n) n 为节点个数
            空间复杂度：O(n) n 为节点个数
      */
      var sumNumbers = function (root) {
        const treeNode = function(root, parentSum) {
          if (root === null) return 0;
          // 每个节点对应一个数字，该数字等于父节点乘以 10 再加上该节点的值，
          const sum = parentSum * 10 + root.val;
          if (root.left === null && root.right === null) {
            return sum;
          } else {
            // 递归循环计算节点对应的数字，然后计算数字总合
            return treeNode(root.left, sum) + treeNode(root.right, sum);
          }
        };

        // 假设根节点对应的数字为 0
        return treeNode(root, 0);
      };
      console.log(sumNumbers([1, 2, 3])); // 25
      console.log(sumNumbers([4, 9, 0, 5, 1])); // 1026
```

# 463. 岛屿的周长

```
      /*
        给定一个包含 0 和 1 的二维网格地图，其中 1 表示陆地 0 表示水域。

        网格中的格子水平和垂直方向相连（对角线方向不相连）。整个网格被水完全包围，但其中恰好有一个岛屿（或者说，一个或多个表示陆地的格子相连组成的岛屿）。

        岛屿中没有“湖”（“湖” 指水域在岛屿内部且不和岛屿周围的水相连）。格子是边长为 1 的正方形。网格为长方形，且宽度和高度均不超过 100 。计算这个岛屿的周长。

        示例 :

        输入:
        [[0,1,0,0], 4 - 1 = 3
        [1,1,1,0], 12 - 4 - 2 = 6
        [0,1,0,0], 4 - 2 = 2
        [1,1,0,0]] 8 - 2 - 1 =  5

        输出: 16
      */
      /**
       * @param {number[][]} grid
       * @return {number}
       */
      /*
        这是 LeetCode 上一位大佬 <> 的解题思路
        https://leetcode-cn.com/problems/island-perimeter/solution/shou-hua-tu-jie-463-dao-yu-de-zhou-chang-by-xiao_b/
        一块陆地有四条边，两块陆地相交，会减掉两个边长
        遍历数组，如果是陆地，就陆地数量递增，如果它的右边或者下边也是陆地，则接边递增
        周长 = 4 * 陆地的数量 - 2 * 减掉的边长
      */
      var islandPerimeter = function (grid) {
        if (!grid) return 0;
        let land = 0, // 陆地数量
          border = 0; // 两块陆地的接边
        for (let i = 0; i < grid.length; i++) {
          for (let j = 0; j < grid[0].length; j++) {
            if (grid[i][j] === 1) { // 判断当前是不是陆地
              land++; // 陆地数量递增
              if (i < grid.length - 1 && grid[i + 1][j] === 1) { // 判断下面是不是陆地
                border++;
              }
              if (j < grid[0].length - 1 && grid[i][j + 1] === 1) { // 判断右面是不是陆地
                border++;
              }
            }
          }
        }
        return 4 * land - 2 * border
      };
      console.log(
        islandPerimeter([
          [0, 1, 0, 0],
          [1, 1, 1, 0],
          [0, 1, 0, 0],
          [1, 1, 0, 0],
        ])
      ); // 16
```
