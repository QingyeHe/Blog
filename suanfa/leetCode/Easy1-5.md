---
title: LC Easy01
author: 何青烨
date: "2022-7-6"
lang: zh-CN
---

<h2>1.两数之和（简单）</h2></br>

给定一个整数数组`nums`和一个整数目标值 `target`，请你在该数组中找出 和为目标值 `target`的那**两个**整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。</br>

**时间复杂度**：_O(N)_，其中 N 是数组中的元素数量。对于每一个元素 `x`，我们可以 _O(1)_ 地寻找 `target - x`。

**空间复杂度**：_O(N)_，其中 N 是数组中的元素数量。主要为哈希表的开销。

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (nums, target) {
  let hash = {};
  for (let i = 0; i < nums.length; i++) {
    if (hash[target - nums[i]] !== undefined) {
      return [i, hash[target - nums[i]]];
    }
    hash[nums[i]] = i;
  }
  return [];
};
```

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashtable = dict()
        for i, num in enumerate(nums):
            if target - num in hashtable:
                return [hashtable[target - num], i]
            hashtable[nums[i]] = i
        return []
```

<h2>2.有效的括号（简单）</h2></br>

给定一个只包括`(`,`)`,`{`,`}`,`[`,`]`的字符串`s`，判断字符串是否有效。

有效字符串需满足：

- 左括号必须用相同类型的右括号闭合。
- 左括号必须以正确的顺序闭合。

**时间复杂度**：_O(n)_，其中 `n` 是字符串 `s` 的长度。

**空间复杂度**：_O(n+∣Σ∣)_，其中 ∣Σ∣ 表示字符集，本题中字符串只包含 6 种括号，∣Σ∣= 6。栈中的字符数量为 _O(n)_，而哈希表使用的空间为 _O(∣Σ∣)_，相加即可得到总空间复杂度。

```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function (s) {
  const n = s.length;
  if (n % 2 === 1) {
    return false;
  }
  const pairs = new Map([
    [")", "("],
    ["]", "["],
    ["}", "{"],
  ]);
  const stk = [];
  for (let ch of s) {
    if (pairs.has(ch)) {
      if (!stk.length || stk[stk.length - 1] !== pairs.get(ch)) {
        return false;
      }
      stk.pop();
    } else {
      stk.push(ch);
    }
  }
  return !stk.length;
};
```

<h2>3.无重复字符的最长字串（中等）</h2>

给定一个字符串`s` ，请你找出其中不含有重复字符的**最长子串**的长度。

**时间复杂度**：_O(N)_，其中 N 是字符串的长度。左指针和右指针分别会遍历整个字符串一次。

**空间复杂度**：_O(∣Σ∣)_，其中*O(∣Σ∣)* 表示字符集（即字符串中可以出现的字符），_O(∣Σ∣)_ 表示字符集的大小。

```js
var lengthOfLongestSubstring = function (s) {
  // 哈希集合，记录每个字符是否出现过
  const occ = new Set();
  const n = s.length;
  // 右指针，初始值为 -1，相当于我们在字符串的左边界的左侧，还没有开始移动
  let rk = -1,
    ans = 0;
  for (let i = 0; i < n; ++i) {
    if (i != 0) {
      // 左指针向右移动一格，移除一个字符
      occ.delete(s.charAt(i - 1));
    }
    while (rk + 1 < n && !occ.has(s.charAt(rk + 1))) {
      // 不断地移动右指针
      occ.add(s.charAt(rk + 1));
      ++rk;
    }
    // 第 i 到 rk 个字符是一个极长的无重复字符子串
    ans = Math.max(ans, rk - i + 1);
  }
  return ans;
};
```

<h2>4.合并两个有序链表（简单）</h2>

将两个升序链表合并为一个新的**升序**链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。

```js
var mergeTwoLists = function (l1, l2) {
  if (l1 === null) {
    return l2;
  }
  if (l2 === null) {
    return l1;
  }
  if (l1.val < l2.val) {
    l1.next = mergeTwoLists(l1.next, l2);
    return l1;
  } else {
    l2.next = mergeTwoLists(l1, l2.next);
    return l2;
  }
};
```

<h2>5.最大子数组和（简单）</h2>

给你一个整数数组`nums` ，请你找出一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

**子数组**是数组中的一个连续部分。

**时间复杂度**：_O(n)_，其中 _n_ 为 _nums_ 数组的长度。我们只需要遍历一遍数组即可求得答案。</br>
**空间复杂度**：_O(1)_。我们只需要常数空间存放若干变量。

```js
var maxSubArray = function (nums) {
  let pre = 0,
    maxAns = nums[0];
  nums.forEach((x) => {
    pre = Math.max(pre + x, x);
    maxAns = Math.max(maxAns, pre);
  });
  return maxAns;
};
```
