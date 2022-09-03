---
title: 岛屿类（DFS）
author: 何青烨
date: "2022-7-11"
lang: zh-CN
---

<h2><a href="https://leetcode.cn/problems/number-of-islands/">岛屿数量（多岛屿）</a></h2>

给你一个由`1`（陆地）和 `0`（水）组成的的二维网格，请你计算网格中岛屿的数量。

```js
var numIslands = function (grid) {
  function dfs(grid, i, j) {
    // 边界判断
    if (
      i < 0 ||
      j < 0 ||
      i >= grid.length ||
      j >= grid[i].length ||
      grid[i][j] == "0"
    )
      return;
    grid[i][j] = 0;
    dfs(grid, i + 1, j);
    dfs(grid, i, j + 1);
    dfs(grid, i - 1, j);
    dfs(grid, i, j - 1);
  }

  var count = 0;
  for (var i = 0; i < grid.length; i++) {
    for (var j = 0; j < grid[0].length; j++) {
      if (grid[i][j] == 1) {
        dfs(grid, i, j);
        count++;
      }
    }
  }
  return count;
};
```

<h2><a href="https://leetcode.cn/problems/island-perimeter/">岛屿的周长（单岛屿）</a></h2>
网格中的格子 水平和垂直 方向相连（对角线方向不相连）。整个网格被水完全包围，但其中恰好有一个岛屿（或者说，一个或多个表示陆地的格子相连组成的岛屿）。格子是边长为 1 的正方形。网格为长方形，且宽度和高度均不超过 100 。计算这个岛屿的周长。

```js
var islandPerimeter = function (grid) {
  function dfs(grid, i, j) {
    // if(i<0||j<0||i>grid.length||j>grid[i].length||grid[i][j]==0) return;

    // 函数因为「坐标 (r, c) 超出网格范围」返回，对应一条黄色的边
    if (i < 0 || j < 0 || i >= grid.length || j >= grid[i].length) {
      return 1;
    }
    // 函数因为「当前格子是海洋格子」返回，对应一条蓝色的边
    if (grid[i][j] == 0) {
      return 1;
    }
    // 函数因为「当前格子是已遍历的陆地格子」返回，和周长没关系
    if (grid[i][j] != 1) {
      return 0;
    }
    grid[i][j] = 2;
    // 继续往四个方向“扩散”，目标是遇到边界和海水，答案随着递归出栈向上返回，得出大的答案
    return (
      dfs(grid, i - 1, j) +
      dfs(grid, i + 1, j) +
      dfs(grid, i, j - 1) +
      dfs(grid, i, j + 1)
    );
  }

  for (var i = 0; i < grid.length; i++) {
    for (var j = 0; j < grid[0].length; j++) {
      if (grid[i][j] == 1) {
        return dfs(grid, i, j);
      }
    }
  }
};
```

<h2><a href="">岛屿的最大面积（多岛屿）</a></h2>

岛屿是由一些相邻的`1`(代表土地) 构成的组合，这里的「相邻」要求两个 `1` 必须在 水平或者竖直的四个方向上 相邻。你可以假设`grid` 的四个边缘都被 `0`（代表水）包围着。岛屿的面积是岛上值为 `1` 的单元格的数目。

计算并返回 `grid` 中最大的岛屿面积。如果没有岛屿，则返回面积为 `0`

```js
var maxAreaOfIsland = function (grid) {
  let count = 0;
  for (let i = 0; i < grid.length; i++) {
    for (let j = 0; j < grid[i].length; j++) {
      if (grid[i][j] === 1) {
        count = Math.max(count, dfs(grid, i, j));
      }
    }
  }
  return count;
};

function dfs(grid, i, j) {
  if (
    i >= grid.length ||
    i < 0 ||
    j >= grid[i].length ||
    j < 0 ||
    grid[i][j] === 0
  )
    return 0;
  grid[i][j] = 0;
  return (
    1 +
    dfs(grid, i + 1, j) +
    dfs(grid, i - 1, j) +
    dfs(grid, i, j + 1) +
    dfs(grid, i, j - 1)
  );
}
```
