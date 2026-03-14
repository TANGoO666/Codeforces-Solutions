## 题目链接：

https://codeforces.com/contest/2183/problem/D1

## 题目描述：

> 给定一颗由 $n$ 个节点组成的树，节点编号 ($1$ ~ $n$)，根节点编号为 $1$  
> 起初，所有节点的颜色都为白色。  
> 现在，我们想把所有节点染成黑色。我们每一次操作可以选择一个节点集 $S$ ，将 $S$ 内所有的节点都染成黑色。
> $S$ 内的节点需满足 **不在同一层** ， 任意节点之间**没有连接** 
> 求 **最少操作次数** 使得树的所有节点都染成黑色

## 核心思路：

令 $x$ 为这棵树对于 **每一层** 最多的节点数， $y$ 为 这棵树每一个由 **父节点+子节点** 形成的集合中 最多的节点数

那么，我们要把整棵树染黑，至少需要 $max(x, y)$ 次操作

这是因为题目要求： “$S$ 内的节点需满足 **不在同一层** ， 任意节点之间**没有连接**”

如果 $x > y$ , 这 $x$ 个节点至少属于不同的 节点集 $S$ ，我们一次只能操作一个节点集 $S$ ，所以要把整棵树染黑，至少需要 $x$ 次操作

如果 $x < y$ ，同理，至少需要 $y$ 次操作

所以，我们要把整棵树染黑，至少需要 $max(x, y)$ 次操作。 更近一步地想，最少操作次数其实就是 $max(x, y)$ 

可以画几棵树验证一下，一定能够在 $max(x, y)$ 次操作把整棵树染黑

## 代码实现：

### 求 x

求 $x$ 可以用 bfs 来求，思路最直观

```cpp
int bfs(int p, vector<vector<int>>& g, vector<bool>& h) {
    int res = 0; queue<int> q;
    h[p] = true; q.push(p);
    while(!q.empty()) {
        int out = (int)q.size();
        res = max(res, out);
        while(out--) {
            int pp = q.front(); q.pop();
            for(auto& x : g[pp]) {if(!h[x]) {h[x] = true; q.push(x);}}
        }
    }
    return res;
}
```

### 求 y

对于根节点，由于根节点没有父节点。因此，由 **根节点** 充当 **父节点+子节点** 形成的集合中，节点数 等于 根节点的 孩子数 + 1（根节点本身）即 `g[根节点].size() + 1`  

对于其他节点，由于它们一定有父节点，因此 由 **这些节点** 充当 **父节点+子节点** 形成的集合中，节点数 等于 该节点的 **度数** 即 `g[该节点].size()` 

## AC Code

```cpp
#include <bits/stdc++.h>
using ll = long long;
using namespace std;

int bfs(int p, vector<vector<int>>& g, vector<bool>& h) {
    int res = 0; queue<int> q;
    h[p] = true; q.push(p);
    while(!q.empty()) {
        int out = (int)q.size();
        res = max(res, out);
        while(out--) {
            int pp = q.front(); q.pop();
            for(auto& x : g[pp]) {if(!h[x]) {h[x] = true; q.push(x);}}
        }
    }
    return res;
}

int main() {
    ios::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);
    int t; cin >> t;
    while(t--) {
        int n; cin >> n;
        vector<bool> h(n + 1); vector<vector<int>> g(n + 1);
        for(int i = 1; i < n; i++) {
            int u, v; cin >> u >> v;
            g[u].push_back(v);
            g[v].push_back(u);
        }
        int ans = bfs(1, g, h);
        for(int i = 1; i <= n; i++) i == 1 ? ans = max(ans, (int)g[1].size() + 1) : ans = max(ans, (int)g[i].size());
        cout << ans << "\n";
    }
}
```