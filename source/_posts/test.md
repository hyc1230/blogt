---
title: test
date: 2023-07-11 12:27:24
tags:
---

这是一个测试。

$1 + 2 = 3$

```cpp
#include <string>
#include <vector>
using namespace std;
#define elif else if

struct trie
{
    constexpr int cid(char c)           // 将字符转换为编号
    {
        return c - 'a' + 1;
    }
    struct node
    {
        char chr;                       // chr为节点（增加）的前缀
        int cld[30];                    // cld[i]为第i个子节点编号
        int prx = 0, wrd = 0;           // prx为节点作为前缀的次数，wrd为节点作为**完整**单词的次数
    };
    int n = 1;                          // n为当前节点数
    vector<node> a = vector<node>(2);   // a为当前节点列表（0号空出，1号为根）

    void insert(string &s)
    {
        int x = 1, p = 0;
        while (p < s.size())
        {
            a[x].prx++;
            if (a[x].cld[cid(s[p])] == 0)
                a.push_back(node()), 
                a[x].cld[cid(s[p])] = ++n;
            x = a[x].cld[cid(s[p])], a[x].chr = s[p++];
            // 注意先更新x！！！
        }
        a[x].prx++, a[x].wrd++;
    }
    int find(string &s)
    {
        int x = 1, p = 0;
        while (p < s.size())
        {
            if (a[x].cld[cid(s[p])] == 0)
                return 0;
            x = a[x].cld[cid(s[p])], p++;
        }
        return a[x].wrd;
    }
};
```