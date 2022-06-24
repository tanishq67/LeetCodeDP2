Question 1: Minimum ASCII Delete Sum for Two Strings { https://leetcode.com/problems/minimum-ascii-delete-sum-for-two-strings/ }

Logic :
```
The idea is to make both the strings equal by deleting some characters. The deletion shoudld be such that we get minimum ascii sum. Which makes sense as if it was the max we would have deleted the whole strings. 
Now, how to proceed. We can think of it as if we choose incdices i and j of the different strings and elements there are not equal then we can either delete one of them or both of them.

dp(i,j) => The minimum ascii sum required to make the string 1 till ith and string 2 till jth equal.
if ith  == jth :
dp(i,j) = dp(i - 1, j - 1);
else:
dp(i,j) = min(dp(i - 1, j) + ascii_val(ith), dp(i, j - 1) + ascii_val(jth), dp(i - 1, j - 1) + ascii_val(jth) + ascii_val(ith));

The reporting answer will be none  other than dp[n][m]
base cases will be dp(0,0) = 0;
and the other will be deleting the whole other string.

C O D E >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

    int ascii(char c){
        return 97 + c - 'a';
    }
    int minimumDeleteSum(string s1, string s2) {
        int n = s1.size(), m = s2.size();
        int dp[n + 1][m + 1];
        memset(dp, 0,sizeof(dp));

        for(int i = 1; i<=n; i++) dp[i][0] = ascii(s1[i - 1]) + dp[i - 1][0]; 
        for(int i = 1; i<=m; i++) dp[0][i] = ascii(s2[i - 1]) + dp[0][i - 1]; 
        
        for(int i = 1; i <= n ; i++){
            for(int j = 1; j <=m ; j++){
                if(s1[i - 1] == s2[j - 1]){
                    dp[i][j] = dp[i -1][j - 1];
                }
                else{
                    dp[i][j] = min({ascii(s1[i - 1]) + dp[i - 1][j],
                                    ascii(s2[j - 1]) + dp[i][j - 1],
                                    dp[i - 1][j - 1] + ascii(s1[i - 1]) + ascii(s2[j - 1])});
                }
            }
        }
        return dp[n][m];
    }
    
```
Question 2: Number of Longest Increasing Subsequence { https://leetcode.com/problems/number-of-longest-increasing-subsequence/ }

Logic :
```


C O D E >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

    
```
Question 3: Largest Divisible Subset { https://leetcode.com/problems/largest-divisible-subset/ }

Logic :
```


C O D E >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

    
```
