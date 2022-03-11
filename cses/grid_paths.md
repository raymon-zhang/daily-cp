# grid_paths
### 3/10/2022
more dp

**state**: only need current position

**transition**: sum of the two cells that can reach, unless blocked then 0

```cpp
#include <bits/stdc++.h>
using namespace std;
 
const int MOD = 1e9+7;
 
int main() {
    ios::sync_with_stdio(0);
    cin.tie(nullptr);
 
    int n;
    cin >> n;
 
    vector<vector<int>> dp(n, vector<int>(n));
 
    for (int i = 0; i < n; i++) {
        string s;
        cin >> s;
        for (int j = 0; j < n; j++) {
            if (i != 0 || j != 0) {
                dp[i][j] = 0;
                if (s.at(j) != '*') {
                    if (i-1 >= 0) {
                        dp[i][j] += dp[i-1][j];
                    }
                    if (j-1 >= 0) {
                        dp[i][j] += dp[i][j-1];
                    }
                }
                dp[i][j] %= MOD;
            } else {
                dp[i][j] = s.at(j) == '*' ? 0 : 1;
            }
        }
    }
 
    cout << dp[n-1][n-1] << "\n";
}
```
