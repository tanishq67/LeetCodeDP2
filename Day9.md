Bomb enemy
```
int maxKilledEnemies(vector<vector<char>> &grid) {
        int n = grid.size(), m = grid[0].size();
        queue<pair<int,int>>q;
        map<pair<int,int>,int> r,c;
        for(int i = 0; i < n ; i++){
            for(int j = 0; j < m; j++){
                if(grid[i][j] !='E' || (r.find({i,j} != r.end() && c.find({i,j}!=c.end()))) continue;
                vector<pair<int,int>> v;
                int cnt = 0;
                for(int k = j ; k < m && grid[i][k]!='W' ; k++){
                    if(grid[i][k] == 'E') v.push_back({i,k}), cnt++;
                } 
                for(int k = j ; k >=0 && grid[i][k]!='W'; k--){
                    if(grid[i][k] == 'E')v.push_back({i,k}), cnt++;
                }
                for(auto& x: v){
                    r[x] = cnt;
                }
                cnt =  0 ;
                v = vector<pair<int,int>>();
                for(int k = i ; k < n & grid[k][j]!='W' ; k++){
                    if(grid[k][j] == 'E') v.push_back({k,j}), cnt++;
                } 
                for(int k = j ; k >=0 && grid[k][j]!='W'; k--){
                    if(grid[k][j] == 'E')v.push_back({k,j}), cnt++;
                }
                for(auto& x: v){
                    c[x] = cnt;
                }
            }
        }
        int ans = 0;
        for(auto i1 : r){
            for(auto i2: c){
                ans = max(ans, (i1.second + i2.second));
            }
        }
        return ans;
        
        



    }
```
