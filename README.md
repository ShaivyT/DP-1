# DP-1

## Problem1 (https://leetcode.com/problems/coin-change/)

// Time Complexity: O(m * n), m = no of coin denominations, n = amount
// Space Complexity: O(m * n), m = no of coin denominations, n = amount

class Solution {
    public int coinChange(int[] coins, int amount) {
        
        int[][] dp = new int[coins.length + 1][amount + 1];
        
        for(int i = 0; i <= coins.length; i++) dp[i][0] = 0;
        for(int j = 1; j <= amount; j++) dp[0][j] = 99999;
        
        for(int i = 1; i <= coins.length; i++) {
            for(int j = 1; j <= amount; j++) {
                
                if(j < coins[i - 1]) {
                    dp[i][j] = dp[i - 1][j];
                } else {
                    dp[i][j] = Math.min(dp[i - 1][j], 1 + dp[i][j - coins[i - 1]]);
                }
            }
        }
        return dp[coins.length][amount] >= 99999 ? -1 : dp[coins.length][amount]; 
    }
}

## Problem2 (https://leetcode.com/problems/house-robber/)

// Time Complexity: O(n)
// Space Complexity: O(n)

class Solution {
    public int rob(int[] nums) {
        
        int n = nums.length;
        if(n == 1) return nums[0];

        int[] dp = new int[n];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0], nums[1]);

        for(int i = 2; i < n; i++) {
            dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i]);
        }

        return dp[n - 1];
    }
}
