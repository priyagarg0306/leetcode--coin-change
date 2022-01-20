# leetcode--coin-change

**----> Question:**

You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin.

 

Example 1:

Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
Example 2:

Input: coins = [2], amount = 3
Output: -1
Example 3:

Input: coins = [1], amount = 0
Output: 0
 

Constraints:

1 <= coins.length <= 12
1 <= coins[i] <= 231 - 1
0 <= amount <= 104

**-----> Code:**

class Solution {

public:

    int coinChange(vector<int>& coins, int amnt) {
        
        int n=coins.size();
        vector<vector<int>> dp(n+1,vector<int>(amnt+1));
        
        for(int i=0;i<=n;i++){
            for(int j=0;j<=amnt;j++){
                if(i==0 && j==0){
                    dp[i][j]=0;
                }else if(i==0){
                    dp[i][j]=INT_MAX-1;
                }else if(j==0){
                    dp[i][j]=0;
                }else if(i==1){
                    if(j%coins[i-1]==0){
                        dp[i][j]=j/coins[i-1];
                    }else{
                        dp[i][j]=INT_MAX-1;
                    }
                }else{
                    if(coins[i-1]<=j){
                        dp[i][j]=min(1+dp[i][j-coins[i-1]],dp[i-1][j]);
                    }else{
                        dp[i][j]=dp[i-1][j];
                    }
                }
            }
        }
        
        if(dp[n][amnt]>amnt){
            return -1;
        }else{
            return dp[n][amnt];
        }
    }
};
