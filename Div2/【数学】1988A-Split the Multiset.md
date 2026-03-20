## 题目链接：

https://codeforces.com/contest/1988/problem/A

## 题目描述：

> 你有一个多重集合 $S$ ，这个多重集合只包含一个正整数 $n$  
> 给定一个正整数 $k$ ，在一次操作中，选择 $S$ 中 任意一个元素 $u$ ，删除 $u$ 的一次出现。  
> 然后在 $S$ 中插入**不超过** $k$ 个正整数，插入的正整数之和等于 $u$  
> 求使 $S$ 包含 $n$ 个 $1$ 的最少操作次数

## 核心思路：

第 $0$ 次操作： $S$ 的长度**最长**为 $1$

第 $1$ 次操作： $S$ 的长度**最长**为 $1 + k - 1 = k$

第 $2$ 次操作： $S$ 的长度**最长**为 $k + k - 1 = 2k - 1$ 

第 $3$ 次操作： $S$ 的长度**最长**为 $(2k - 1) + k - 1 = 3k - 2$

第 $x$ 次操作： $S$ 的长度**最长**为 $xk - (x - 1)$ 

最终 $S$ 包含 $n$ 个 $1$ ，即 $S$ 的长度为 $n$ 

由：

$$
xk - (x - 1) ≥ n
$$

解得：

$$
x ≥ \dfrac{n - 1}{k - 1}
$$

由于 $x$ 是整数，因此结果**向上取整** 

## AC Code

```cpp
#include <iostream>
#include <vector>
#include <map>
#include <set>
#include <algorithm>
using ll = long long;
using namespace std;

int main() {
    ios::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);
    int t; cin >> t;
    while (t--) {
        int n, k; cin >> n >> k;
        (n - 1) % (k - 1) == 0 ? cout << (n - 1) / (k - 1) << "\n" : cout << (n - 1) / (k - 1) + 1 << "\n";
    }
}
```