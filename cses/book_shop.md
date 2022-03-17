# book_shop
### 3/11/2022
i did this on 3/11 but forgot to post it

also dp, 0-1 knapsack

**state**: you need to know the price, and the last book used

**transition**: if you bought book `k`, the new price is `i + h[k]`, and the amount of pages is `dp[i] + s[k]`

to turn this into pull dp, for every price `i`, you should max `dp[i]` with `dp[i-h[k]] + s[k]`

essentially, you consider the books one by one, given book `k`, you loop backwards through all prices `i`, if you buy book `k`, you get `s[k]` pages, thus it is now possible to get `dp[i-h[k]] + s[k]` pages with max price `i`.

`dp[i]` represents the maximum number of pages you can get with price at most `i`, considering only the first `k` books.
```cpp
#include <bits/stdc++.h>
using namespace std;
 
const int MOD = 1e9+7;
 
int main() {
    ios::sync_with_stdio(0);
    cin.tie(nullptr);
 
    int n, x;
    cin >> n >> x;
    vector<int> h(n);
    for (int& i: h) {
        cin >> i;
    }
    vector<int> s(n);
    for (int& i: s) {
        cin >> i;
    }
 
    vector<int> dp(x+1);
    
    for (int k = 0; k < n; k++) {
        for (int i = x; i >= h[k]; i--) {
            dp[i] = max(dp[i-h[k]] + s[k], dp[i]);
        }
    }
 
    cout << dp[x] << "\n";
}
```
