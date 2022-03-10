# coin_combinations
### 3/8/2022
classical dp problem

**state**: u only need to know the current sum

**transition**: to transition, add all of the possible states that can reach the current state

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
 
    vector<int> dp(x+1);
    dp[0] = 1;
 
    for (int i = 1; i <= x; i++) {
        for (int c: coins) {
            if (i-c >= 0) {
                dp[i] += dp[i-c];
                dp[i] %= MOD;
            }
        }
    }
 
    cout << dp[x] << "\n";
}
```
