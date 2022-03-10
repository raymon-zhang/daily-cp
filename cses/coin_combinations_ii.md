# coin_combinations_ii
### 3/8/2022
dp

**state**: `dp[k][i]` is the number of ways to make `i` using the first `k` coins

**transition**: there are two transitions, either the current coin gets used once or it stops getting used

```cpp
#include <bits/stdc++.h>
using namespace std;
 
const int MOD = 1e9+7;
 
int main() {
    ios::sync_with_stdio(0);
    cin.tie(nullptr);
 
    int n, x;
    cin >> n >> x;
 
    vector<int> coins;
    for (int i = 0; i < n; i++) {
        int y;
        cin >> y;
        coins.push_back(y);
    }
 
    vector<vector<int>> dp(n+1, vector<int>(x+1));
    dp[0][0] = 1;
 
    for (int k = 1; k <= n; k++) {
        for (int i = 0; i <= x; i++) {
            dp[k][i] += dp[k-1][i];
            if (i-coins[k-1] >= 0) {
                dp[k][i] += dp[k][i-coins[k-1]];
            }
            dp[k][i] %= MOD;
        }
    }
 
    cout << dp[n][x] << "\n";
}
```
