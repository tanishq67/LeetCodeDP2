Question 1: Product of Array Except Self { https://leetcode.com/problems/product-of-array-except-self/ }

Logic :
```
no big deal. Just use the associative property of multiplication. Break the problem in left and right portions make them like prefix multiplication and solve them.
---------------------------------------------------------------------
    vector<int> productExceptSelf(vector<int>& nums) {
        int l = 1, r = 1; int n = nums.size();
        vector<int> left, right;
        for(int i = 0 ; i < n ; i++){
            left.push_back(l);
            l *= nums[i];
        }
        for(int i = n - 1; i >= 0 ; i--){
            right.push_back(r);
            r *= nums[i];
        }
        vector<int> ans(n);
        for(int i = 0 ; i < n ; i++){
            ans[i] = left[i]*right[n - i - 1];
        }
        return ans;
    }
```
Question 2:  Longest Line of Consecutive One in Matrix { https://www.lintcode.com/problem/875/ }

Logic :
```
Same as above this time break down the problem into 4 parts diagonal anti digonal vertical and horzontal and then get the max answer from them. The final max will
be the answer.
---------------------------------------------------------------------
    int longestLine(vector<vector<int>> &mat) {
        if(mat.size() == 0) return 0;
        int n = mat.size(), m = mat[0].size();
        
        vector<vector<int>> h(n, vector<int>(m,0)), v(n, vector<int>(m,0)),
                            d(n, vector<int>(m,0)), a(n, vector<int>(m,0));
        int mx = 0;

        for(int i  = 0 ; i < n; i++) h[i][0] = mat[i][0], mx = mat[i][0];  
        for(int i = 0 ; i < n ; i++){
            for(int j =  1;  j < m; j++){
                if(mat[i][j] == 1) h[i][j] = h[i][j - 1] + 1;
                else h[i][j] = 0;
                mx = max(mx, h[i][j]); 
                cout<<h[i][j]<<" ";
            }
            cout<<"\n";
        } 

        for(int j = 0 ; j < m; j++) v[0][j] = mat[0][j],mx = max(mx,mat[0][j]);
        for(int j = 0 ; j < m; j ++){
            for(int i = 1 ;i < n; i++){
                if(mat[i][j] == 1) v[i][j] = v[i - 1][j] + 1;
                else v[i][j] = 0;       
                mx = max(mx, v[i][j]);
            cout<<v[i][j]<<" ";
            }
            cout<<"\n";
        }

        for(int i = 0; i < n ; i++) d[i][0] = mat[i][0];
        for(int i = 0 ; i < m ; i++) d[0][i] = mat[0][i];
        for(int j = 1 ; j < m; j ++){
            for(int i = 1 ;i < n; i++){
                if(mat[i][j] == 1) d[i][j] = d[i - 1][j - 1] + 1;
                else d[i][j] = 0;       
                mx = max(mx, d[i][j]);
                cout<<d[i][j]<<" ";
            }
            cout<<"\n";
        }
        for(int i = 0 ; i < m ; i++) a[0][i] = mat[0][i];
        for(int i = 0 ; i < n ; i++) a[i][m - 1] = mat[i][m - 1];
        for(int j = 0 ; j < m - 1; j ++){
            for(int i = 1 ;i < n; i++){
                if(mat[i][j] == 1) a[i][j] = a[i - 1][j + 1] + 1;
                else a[i][j] = 0;       
                mx = max(mx, a[i][j]);
                cout<<a[i][j]<<" ";
            }
            cout<<"\n";
        }
        return mx;
    }
```
