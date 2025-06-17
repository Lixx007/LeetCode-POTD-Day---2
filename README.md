# 3405. Count the Number of Arrays with K Matching Adjacent Elements

<img src="https://miro.medium.com/v2/resize:fit:700/format:webp/1*VOQU8CuPG34Gsd1yJCadOQ.png" width="500"/>

## ✅ C++ Code

```cpp
class Solution {
public:
    int MOD = 1e9 + 7;

    int countGoodArrays(int n, int m, int k) {
        vector<vector<int>> dp(n + 1, vector<int>(k + 1, 0));

        // Base case: arrays of size 1 can only have 0 adjacent matches
        dp[1][0] = m;

        // Loop from size 2 to n
        for (int i = 2; i <= n; i++) {
            for (int j = 0; j <= k; j++) {
                
                // Case 1: Make current value same as previous (add a match)
                if (j - 1 >= 0) {
                    dp[i][j] += dp[i - 1][j - 1];
                    dp[i][j] %= MOD;
                }

                // Case 2: Make current value different from previous (no match added)
                dp[i][j] += (1LL * dp[i - 1][j] * (m - 1)) % MOD;
                dp[i][j] %= MOD;
            }
        }

        return dp[n][k];
    }
};
