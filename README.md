# DP-1

## Problem1: Coin Change

```Java
class Solution {
    public int change(int amount, int[] coins) {
        //null check
        if(coins == null || coins.length == 0) return 0;
        
        int m = coins.length; 
        int n = amount;
        
        int[][] dp = new int[m+1][n+1];
        dp[0][0] = 0;
        
        //top row
        for(int j=1;j<dp[0].length;j++){
            dp[0][j] = amount+1;
        }
        
        for(int i=1;i<dp.length;i++){
            for(int j=1;j<dp[0].length;j++){
                //till amount is not equal to denomination
                //not choose case
                if(j<coins[i-1]){
                    dp[i][j] = dp[i-1][j];
                }
                else{
                    dp[i][j] = Math.min(dp[i-1][j], dp[i][j-coins[i-1]] + 1);
                }
            }
        }
        int result = dp[m][n];
        
        if(result > amount)
            return -1;
        
        return result;
    }
}
```

## Problem2: House Robber

```Java
class Solution {
    public int rob(int[] nums) { 
        if(nums == null || nums.length == 0)
            return 0;
        
        int n = nums.length;  
        int[] dp = new int[n];
        
        //if there exists just one house -> rob it
        if(n == 1)
            return nums[0]; 
        
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0], nums[1]);
        
        for(int i=2;i<n;i++){
            dp[i] = Math.max(dp[i-1], nums[i]+dp[i-2]);
        }
        return dp[n-1];
    }
}
```

