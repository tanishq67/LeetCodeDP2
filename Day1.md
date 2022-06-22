Question 1: Paint House { https://www.lintcode.com/problem/515/ } 


Logic : 

```
Lets think of the problem as we are trying to solve it by parts 
first my dp(i) will tell me what is the minimum cost that is required to get i houses painted
now lets say I have dp(i) then for me to paint the dp(i + 1) I need one more information that will be which was the last house painted with with 

Now, my state changed up to dp(i,ith color). For dp(i+1, ith color) = min of {dp(i, allowed colors) + ith color cost}.
MY Final reporting answer will be none other than, min of dp(n, all colors)

C O D E >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

    int minCost(vector<vector<int>> &cost) {
        int n = cost.size(); if(n == 0) return 0;
        int dp[n][3];
        memset(dp, 0, sizeof(dp));
        dp[0][0] = cost[0][0]; dp[0][1] = cost[0][1]; dp[0][2] = cost[0][2];
        for(int i =1 ; i<n ; i++){
            dp[i][0] = min(dp[i - 1][1], dp[i-1][2]) + cost[i][0];
            dp[i][1] = min(dp[i - 1][0], dp[i-1][2]) + cost[i][1];
            dp[i][2] = min(dp[i - 1][0], dp[i-1][1]) + cost[i][2];
        } 
        return min({dp[n-1][0], dp[n - 1][1], dp[n - 1][2]});
    } 
```

Question 2: 
