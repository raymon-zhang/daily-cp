# array_description
### 3/16/2022
i was busy, definitely didn't forget lol

we need to know the current position `i`, and the value in the array at index `i`

`dp[i][j]` = the number of arrays up to index `i`, assuming `x[i] = j`

for `i = 0`, if `x[0]` = 0, then `dp[0][k] = 1` for all k, otherwise `dp[0][x[0]]` is 1, and the rest are 0

**transition**: for every other i from 1 to n-1, if `x[i]` = 0, then for all k, `dp[i][k]` is the sum of `dp[i][k-1]`, `dp[i][k]`, `dp[i][k+1]`.
otherwise, `dp[i][x[i]]` is the sum of `dp[i][x[i]-1]`, `dp[i][x[i]]`, `dp[i][x[i]+1]`.

```cpp
#include <bits/stdc++.h>
using namespace std;
 
const int MOD = 1e9+7;
 
int main() {
    ios::sync_with_stdio(0);
    cin.tie(nullptr);
 
    int n, m;
    cin >> n >> m;
    vector<vector<int>> dp(n, vector<int>(m+1));
 
    int x;
    cin >> x;
    if (x == 0) {
        fill(dp[0].begin(), dp[0].end(), 1);
    } else {
        dp[0][x] = 1;
    }
 
    for (int i = 1; i < n; i++) {
        cin >> x;
        if (x == 0) {
            for (int j = 1; j <= m; j++) {
                if (j-1 >= 1 && j-1 <= m) {
                    dp[i][j] += dp[i-1][j-1];
                    dp[i][j] %= MOD;
                }
                if (j >= 1 && j <= m) {
                    dp[i][j] += dp[i-1][j];
                    dp[i][j] %= MOD;
                }
                if (j+1 >= 1 && j+1 <= m) {
                    dp[i][j] += dp[i-1][j+1];
                    dp[i][j] %= MOD;
                }
            }
        } else {
            if (x-1 >= 1 && x-1 <= m) {
                dp[i][x] += dp[i-1][x-1];
                dp[i][x] %= MOD;
            }
            if (x >= 1 && x <= m) {
                dp[i][x] += dp[i-1][x];
                dp[i][x] %= MOD;
            }
            if (x+1 >= 1 && x+1 <= m) {
                dp[i][x] += dp[i-1][x+1];
                dp[i][x] %= MOD;
            }
        }
    }
 
    int ans = 0;
    for (int i = 1; i <= m; i++) {
        ans += dp[n-1][i];
        ans %= MOD;
    }
 
    cout << ans << "\n";
}
```
