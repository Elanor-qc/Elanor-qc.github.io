---
title: "STL拾遗"
description: "如题"
pubDatetime: 2026-07-29T12:00:00+08:00
tags:
  - Note
  - Study
  - Tech
featured: false
draft: false
---

整理一些常见的 STL 语法放在这里——

---

# vector

```cpp

#include <vector>
vector<int> nums;                    // 初始化
vector<int> v(5, 0);                 // 大小为5，填充0
vector<int> v2 = {1, 2, 3};          // 列表初始化

// 常用操作
v.size();          // 长度 (返回 size_t，注意转 int 时强转)
v.push_back(4);    // 尾部插入
v.pop_back();      // 尾部删除
v.empty();         // 判空
v.clear();         // 清空
v.begin(); v.end();// 迭代器（配合算法）
v[0]; v.at(0);     // 访问（at会检查越界，刷题多用 [] 快）

// 重点：二维数组（邻接表/矩阵）
vector<vector<int>> matrix(m, vector<int>(n, 0)); 

```

vector是我们的老朋友！ヾ(≧▽≦*)o

---

# 哈希表 `unordered_map` / `unordered_set`

O(1)查找！这是它们最大的优势ovo

```cpp

#include <unordered_map>
#include <unordered_set>

unordered_map<string, int> mp;
mp["key"] = 10;                     // 插入/修改
mp.count("key");                    // 判断是否存在（返回 0/1）
mp.find("key");                     // 查找，返回迭代器（不存在返回 mp.end()）
if (mp.find("key") != mp.end()) {}

// 取值陷阱
int val = mp["key"];                // 如果 key 不存在，会插入默认值 0！
// 安全做法：先 find 再取值，或用 at()
int val = mp.at("key");             // 不存在抛异常

// unordered_set 常用
unordered_set<int> set;
set.insert(5);
set.count(5);                       // 查重

```

---

# `stack` 和 `queue`

```cpp

#include <stack>
#include <queue>

stack<int> st;
st.push(1); st.top(); st.pop(); st.empty();

queue<int> q;
q.push(1); q.front(); q.back(); q.pop(); q.empty();

// 双端队列（滑动窗口专用）
deque<int> dq;
dq.push_back(); dq.push_front(); dq.pop_back(); dq.pop_front();

```

---

# priority_queue

```cpp

#include <queue>
// 默认是大顶堆（最大堆）
priority_queue<int> pq; 
pq.push(3); pq.top(); pq.pop();

// 小顶堆（最小堆）写法
priority_queue<int, vector<int>, greater<int>> minHeap;

// 自定义结构体比较（刷题常用 Lambda 构造）
auto cmp = [](int a, int b) { return a > b; }; // 注意：return true 时 a 优先级低
priority_queue<int, vector<int>, decltype(cmp)> pq(cmp);

```

