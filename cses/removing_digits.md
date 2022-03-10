# removing_digits
### 3/9/2022

**state**: only need current number

**transition**: test each of the digits, subtract each of them and see which is the lowest

```cpp
#include <bits/stdc++.h>
using namespace std;

const int MOD = 1e9+7;

int main() {
    ios::sync_with_stdio(0);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vector<int> dp(n+1);

    for (int i = 1; i <= n; i++) {
        int j = i;
        dp[i] = 1000000000;
        while (j != 0) {
            dp[i] = min(dp[i], dp[i - j%10]);
            j/=10;
        }
        dp[i]++;
    }

    cout << dp[n] << "\n";
}
```
