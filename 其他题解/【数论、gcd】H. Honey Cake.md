## 题目链接：

https://codeforces.com/contest/2181/problem/H

## 题目描述：

> 现有一个尺寸为 $w×h×d$ 的蛋糕  
> 给定一个 正整数 $n$，这个蛋糕能够切割成 $n$ 份吗？  
> （每条边等分切割，且每块的长度都是整数）  
> （切割  $0$ 次是合法的）

## 核心思路：

假设 $w$ 分成了 $x$ 份， $h$ 分成了 $y$ 份， $d$ 分成了 $z$ 份

那么， $x×y×z = n$ 

即：

$x \;|\; w$ 并且 $x \;|\; n$ 

$y \;|\; h$ 并且 $y \;|\; n$ 

$z \;|\; d$ 并且 $z \;|\; n$ 

即：

$x$ 是 $w$ 和 $n$ 的公因子

$y$ 是 $h$ 和 $n$ 的公因子

$z$ 是 $d$ 和 $n$ 的公因子

我们让 $w$ 和 $h$ 和 $d$ 尽可能地多分几份 (使得能够把蛋糕分成 $n$ 份的成功率最高)

所以，使用 `gcd()` 获取每条边能够分割的最大份数

```cpp
	ll x = gcd(w, n); n /= x;
    ll y = gcd(h, n); n /= y;
    ll z = gcd(d, n); n /= z;
```

$$
n_{1} = \dfrac{n}{x}
$$

$$
n_{2} = \dfrac{n_{1}}{y} = \dfrac{n}{xy}
$$

$$
n_{3} = \dfrac{n_{2}}{z} = \dfrac{n}{xyz}
$$

若 $n_{3} = 1$  

即 $1 = \dfrac{n}{xyz}$ 

即 $x×y×z = n$ ， 说明蛋糕能够分成 $n$ 份

**注意**：题目求的是每条边的切割数，切割数 等于 分成的份数 - 1

## AC Code

```cpp
#include <bits/stdc++.h>
using ll = long long;
using namespace std;

int main() {
    ios::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);
    ll w, h, d; cin >> w >> h >> d;
    ll n; cin >> n;
    ll x = gcd(w, n); n /= x;
    ll y = gcd(h, n); n /= y;
    ll z = gcd(d, n); n /= z;
    n == 1 ? cout << x-1 << " " << y-1 << " " << z-1 : cout << -1;
}
```