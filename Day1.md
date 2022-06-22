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

Question 2: Paint House II { https://www.lintcode.com/problem/516/ } 
Logic : 

```
Pretty similar nothing else to think more in this problem. except for the hardcoding we have to write a loop. 
But if I will continue to solve it trivially, it may bump my complexity to O(n*k*k). I have to thinking something 
smart enough to predict the min of last dp(i, over all colors except ours) that will be simply done by keeping 2 mns the 
most min and the second most. If our number is equal to most one we will choose secone most one easy. 10 iq question.

C O D E >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

    int minCostII(vector<vector<int>> &cost) {
        if(cost.size() == 0)return 0;
        int n = cost.size(), k = cost[0].size(); 
        int dp[n][k];
        memset(dp, 0, sizeof(dp));
        int mn = 1e9, mn2 = 1e9;
        for(int i = 0 ; i < k; i++) {
            dp[0][i] = cost[0][i];
            if(mn > dp[0][i]) mn2 = mn, mn = dp[0][i];
            else mn2 = min(dp[0][i], mn2);
        } 
        for(int i =1 ; i<n ; i++){
            int newmn = 1e9, newmn2 = 1e9;
            for(int j = 0 ; j<k; j++){
                dp[i][j] = cost[i][j];
                if(dp[i-1][j] == mn) dp[i][j] += mn2;
                else dp[i][j] += mn;
                if(newmn > dp[i][j]) newmn2 = newmn, newmn = dp[i][j];
                else newmn2 = min(dp[i][j], newmn2);
            }
            mn = newmn; mn2 = newmn2;
        } 
        int ans = 1e9;
        for(int i = 0 ;  i < k ; i++) ans = min(ans, dp[n-1][i]);
        return ans;
    }
```

Question 3: Max Consecutive Ones II { https://www.lintcode.com/problem/883/ } 
Logic : 
```
A simple method will be to get vector in pair form and then just whenever the i + 2 == '1' and i + 1 == '0' and size = 1 add them up. 
A dp way will be to think if we will shift this 0 what effect will be on the answer. 
dp(i) -> the max number of consectutive uptill i 
then if it is 0 then we will switch how will we be able to keep the count that we have switched. 
Hence, new dp will be dp(i, used the ability? )
the answer will be simply the max(dp(n,0) , dp(n,1))

if this is 0 then 
dp(i, not used == 0 ) = dp(i - 1, 0)
dp(i, used ) = max(dp(i - 1,0) + .....

AS we can see here we are facing a dilema, as it is visbily confusing to tell if in this dp state if last was a streak and increament.
So, lets change our dp defination and now my dp will be 
dp(i, used) => the current streak. 
So final answer will be max({among all dp states})

Now, 
if 0 : dp(i, used)  = dp(i - 1, !used) + s[i-1]==1 ; dp(i,!used) = 0;
if 1 : dp(i,used) = dp(i - 1, used) + 1; dp(i,!used) = dp(i - 1, !used) + 1; 


C O D E >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
    int findMaxConsecutiveOnes(vector<int> &s) {
        int n = s.size(); if(n == 0) return 0;
        int dp[n][2];
        memset(dp,0,sizeof(dp));
        dp[0][1] = 1; dp[0][0] = (s[0] == 1); 
        for(int i = 1; i < n ; i++){
            if(s[i] == 1){
                dp[i][1] = dp[i - 1][1] + 1; dp[i][0] = dp[i - 1][0] + 1;
            }
            else{
                dp[i][1] = dp[i - 1][0] + (s[i - 1] == 1); dp[i][0] = 0;
            }
        }

        int ans = 0; 
        for(int i = 0; i<n; i++) ans = max({ans, dp[i][0], dp[i][1]});
        return ans;
    }
```
