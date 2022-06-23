Question 1: Toss strange coins { https://www.codingninjas.com/codestudio/problems/toss-strange-coins_1459385 }

Logic :
```

C O D E >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

```
Question 2: Uncrossed Lines { https://leetcode.com/problems/uncrossed-lines/ }

Logic :
```
Lets say my dp(i,j) is the amount of uncrossed lines I managed to draw using ith aray and jth array of the 
subsequent array.
if ith == jth:  dp(i,j) = max(dp(i - 1, j), dp(i, j - 1), dp(i - 1, j - 1) + 1) ;
else dp(i,j) = max(dp(i - 1, j), dp(i, j - 1))
That means we can directly join the two 
Anything else to consider lets dry run and see -- to understand the question better

1 4 2                     0 0 0 0 
1 2 4                     0 1 1 1
                          0 1 1 2
                          0 1 2 **2**
This seems legit to me.

C O D E >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

    int maxUncrossedLines(vector<int>& nums1, vector<int>& nums2) {
        int n = nums1.size(), m = nums2.size();
        int dp[n + 1][m + 1];
        memset(dp, 0, sizeof(dp));
        
        for(int i = 1 ; i <= n; i++){
            for(int j = 1; j<=m; j++){
                dp[i][j] = max(dp[i - 1][j] , dp[i][j - 1]);
                if(nums1[i - 1] == nums2[j - 1])
                    dp[i][j] = max(dp[i][j],dp[i - 1][j - 1] + 1);
            }
        }

        return dp[n][m];
    }
    
```
