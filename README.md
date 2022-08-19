# Solve-N-puuzle
#include <iostream>
#include <vector>
#include <string>

using namespace std;
int K = 0;

vector<vector<int>> make_vec(string s){
    vector<vector<int>> C;
    
    for(int i=0;i<3;i++){
        vector<int> v;
        for(int j=0;j<3;j++){
            int x = int(s[i*3 + j]) - 48;
            v.push_back(x);
        }
        C.push_back(v);
    }
    
    return C;
}


void chk(vector<vector<int>> S, vector<vector<int>> &T, int g, int parg, int av, int ans){
    int r = 0;
    int x = 0;
    int y = 0;
    int n = S.size();
    for(int i=0;i<n;i++){
        for(int j=0;j<n;j++){
            if(S[i][j]!=T[i][j]) r++;
            
            if(S[i][j]==0){
                x = i;
                y = j;
            }
        }
    }
    
    if(r==0){
        K = ans;
        return ;
    }
    
    r = r + g;
    
    if(r>parg) return ;
    
    
    if(x-1>=0 && av!=1){
        int t = S[x-1][y];
        S[x-1][y] = S[x][y];
        S[x][y] = t;
        
        chk(S,T,g+1,r,3,ans+1);
        
        t = S[x-1][y];
        S[x-1][y] = S[x][y];
        S[x][y] = t;
    }
    
    if(y-1>=0 && av!=2){
        int t = S[x][y-1];
        S[x][y-1] = S[x][y];
        S[x][y] = t;
        
        chk(S,T,g+1,r,4,ans+1);
        
        t = S[x][y-1];
        S[x][y-1] = S[x][y];
        S[x][y] = t;
    }
    
    if(x<n-1 && av!=3){
        int t = S[x+1][y];
        S[x+1][y] = S[x][y];
        S[x][y] = t;
        
        chk(S,T,g+1,r,1,ans+1);
        
        t = S[x+1][y];
        S[x+1][y] = S[x][y];
        S[x][y] = t;
    }
    
    if(y<n-1 && av!=4){
        int t = S[x][y+1];
        S[x][y+1] = S[x][y];
        S[x][y] = t;
        
        chk(S,T,g+1,r,2,ans+1);
        
        t = S[x][y+1];
        S[x][y+1] = S[x][y];
        S[x][y] = t;
    }
    
    return ;
    
    
}

int main()
{
    string s = "283164705";
    
    string t = "836210754";
    
    
    vector<vector<int>> S = make_vec(s);
    vector<vector<int>> T = make_vec(t);
    
    
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            cout << S[i][j] << "   ";
        }
        cout << "     "  ;
        for(int j=0;j<3;j++){
            cout << T[i][j] << "   ";
        }
        cout << endl;
    }
    
    
    
    int ans = 0;
    int g = 0;
    K = 0;
    chk(S,T,g,1000,-1,ans);
    cout << endl;
    cout << endl;
    cout << K;


    return 0;
}
