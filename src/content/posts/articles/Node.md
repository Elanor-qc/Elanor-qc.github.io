---
title: "链表（1）"
description: "一些基本的理论知识"
pubDatetime: 2026-07-25T12:00:00+08:00
tags:
  - Note
  - Study
  - Tech
featured: false
draft: false
---

链表理论上是计概A的内容，但是由于苯人习惯翘课＆期末考试并不涉及，这一块当时就没有学。。。从头学起吧！

以一道LC题目串联一下链表的经典操作。


---

# 题目描述

## 707.设计链表

### 实现 `MyLinkedList` 类：

- `MyLinkedList()` 初始化 `MyLinkedList` 对象。
- `int get(int index)` 获取链表中下标为 `index` 的节点的值。如果下标无效，则返回 -1 。
- `void addAtHead(int val)` 将一个值为 `val` 的节点插入到链表中第一个元素之前。在插入完成后，新节点会成为链表的第一个节点。
- `void addAtTail(int val)` 将一个值为 `val` 的节点追加到链表中作为链表的最后一个元素。
- `void addAtIndex(int index, int val)` 将一个值为 `val` 的节点插入到链表中下标为 `index` 的节点之前。如果 `index` 等于链表的长度，那么该节点会被追加到链表的末尾。如果 `index` 比长度更大，该节点将 **不会插入** 到链表中。
- `void deleteAtIndex(int index)` 如果下标有效，则删除链表中下标为 `index` 的节点。
 

### 提示：

0 <= `index`,` val` <= 1000

请不要使用内置的 `LinkedList` 库。


---


# 解答

我们采用虚拟头节点来实现这几个接口~

```cpp

class MyLinkedList {
    struct LinkedNode{
        int val;
        LinkedNode* next;
        LinkedNode(int val):val{val},next{nullptr}{};
    };
//struct后面记得加分号qwq...

    int _size;
    LinkedNode* _dummyHead;


public:
    MyLinkedList() {
        _dummyHead = new LinkedNode(0);
        _size = 0;        
    }
    
    int get(int index) {
        if(index>(_size-1)||index<0){
            return -1;
        }
        LinkedNode* cur = _dummyHead->next;
        while(index--){
            cur = cur->next;
        }
        return cur->val;
    }
    
    void addAtHead(int val) {
        LinkedNode*  newNode = new LinkedNode(val);
        newNode->next = _dummyHead->next;
        _dummyHead->next = newNode;
        _size++;
    }
   //其实都是极其类似的写法！->next 用以传到下一个
    
    void addAtTail(int val) {
        LinkedNode* newNode = new LinkedNode(val);
        LinkedNode* cur = _dummyHead;
        while(cur->next!=nullptr){
            cur = cur->next;
        }
        cur->next = newNode;
        _size++;
    }
    
    void addAtIndex(int index, int val) {
        if(index > _size) return;
        LinkedNode* newNode = new LinkedNode(val);
        LinkedNode* cur = _dummyHead;
        while(index--){
            cur = cur->next;
        }
        newNode->next = cur->next;
        cur->next = newNode;
        _size++;
    }
    //这里注意，是index--（先判断再自减）而不是--index；由于我们引入了虚拟头，而用户看到的有效链表仍然是从0开始计算，可以认为虚拟头处的index=-1    


    void deleteAtIndex(int index) {
        if(index>=_size||index<0) return;
        LinkedNode* cur = _dummyHead;
        while(index--){
            cur = cur->next;
        }
        LinkedNode* tmp = cur->next;
        cur->next = cur->next->next;
        delete tmp;
        _size--;
    }
   //每次插入/删除完毕后记得更新_size!
};

```


