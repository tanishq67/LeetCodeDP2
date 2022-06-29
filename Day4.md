Question 1: Longest string chain { https://leetcode.com/problems/longest-string-chain/ }

Logic :
```
Dont have to generate the answer so its quiet trivial and similar to that of increasing subsequence. Lets move on to solve the question. 

Dp(i) => The max number of word chain that can be made with the ith set of words with ith used.
traverse the previous ones and update. Final answer will be max(dp). 
To update the count we need to pay careful attention that will be first check if the word is one less than prev in length after that we just see if smaller is
the subseq of the larger one.

IMP Takeaways --> use static in mycomp  and & is very important for speed. 
---------------------------------------------------------------------
    static bool mycomp(string& s1, string& s2){
        return s1.size()<s2.size();
    }
    int longestStrChain(vector<string>& words) {
        int n = words.size();
        sort(words.begin(), words.end(), mycomp);
        vector<int> dp(n, 1);
        
        for(int i  = 0 ; i < n; i ++){
            for(int j  = i - 1; j>=0 ; j--){
                string& w1 = words[j], &w2 = words[i];
                if(w1.size() + 1 != w2.size())continue;
                int k = 0; for(char c: w2){ if(c == w1[k]) k++;}
                if(k != w1.size())continue;
                dp[i] = max(dp[i],dp[j] + 1);
            }
        }
        
        int mx = 1;
        for(int x: dp) mx = max(mx,x);
        return mx;
    }
```

Question 2: maximum length of pair chain { https://leetcode.com/problems/maximum-length-of-pair-chain/ }

Logic :
```
Again a same concept. Nothing special

---------------------------------------------------------------------
    bool check(vector<int>&x, vector<int>&y){
        if(x[1] < y[0])
            return true;
        return false;
    }
    int findLongestChain(vector<vector<int>>& pairs) {
        int n = pairs.size();
        vector<int> dp(n, 1);
        sort(pairs.begin(), pairs.end());
        for(int i = 0 ; i < n ; i++){
            for(int j = 0 ; j < i; j++){
                if(check(pairs[j], pairs[i]))
                    dp[i] = max(dp[i], dp[j] + 1);
            }
        }
        
        int mx = 1; for(int x: dp)mx = max(mx,x);
        return mx;
    }
```
