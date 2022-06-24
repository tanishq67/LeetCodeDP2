Question 1: Toss strange coins { https://www.codingninjas.com/codestudio/problems/toss-strange-coins_1459385 }

Logic :
```
The idea is to get exactly target number of coins get heads and rest get the opposite. And add up all the scenerios.
The trival way will be to produce everything. 
Example we have 4 coins and target is 3 
_ _ _ _
+ + + - 
+ + - +
+ - + +
- + + + 
Add all these posiblites. A simple bruteforce way. 
complexity will be nCtarget hence of the form 2powern 
This is exactly similar to knapsack where we give choice of to either take or leave. 
here if we will choose to leave we will instead multiply the anti probability.

Let Dp(i,j) => will tell me the probability of getting j heads with i coins.
Hence, my reporting answer will be none other than Dp(n, target)

My fundamental reccurence --> dp(i,j) = dp(i - 1, j - 1)*Prob[i] + dp(i-1, j)*(1 - Prob[i]) ;

Base cases to keep in mind, dp(0,j) is always 0. However, dp(i,0) is multiplication of the anti probablity.
While dp(0,0) == 1 ;
C O D E >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

double tossStrangeCoins(vector<double> &prob, int target){
    int n = prob.size();
	double dp[n + 1][target + 1];
    dp[0][0] = 1;
    for(int j = 1 ; j <= target ; j++) dp[0][j] = 0;
    for(int i = 1; i <= n ; i++){
        dp[i][0] = dp[i - 1][0] * ( 1- prob[i - 1]);
    }
    for(int i = 1 ; i <= n ; i++){
        for(int j = 1; j<=target; j++){
            dp[i][j] = (dp[i - 1][j - 1] * prob[i - 1]) + ((dp[i - 1][j ]) * ( 1 - prob[i - 1])) ; 
        }
    }
    return dp[n][target];
}

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
