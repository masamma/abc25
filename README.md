# abc25
#include<iostream>
#include<algorithm>
#include<vector>
#include<queue>
#include<map>
#include<set>
#include<string>
#include<stack>
#include<cstdio>
#include<cmath>
#include<iomanip>
using namespace std;
 
typedef long long ll;
typedef long double ld;
typedef pair<int,int> pii;
typedef pair<int,pii> piii;
typedef vector<int> vi;
typedef vector<pii> vpii;
 
#define fr first
#define sc second
#define mp make_pair
#define pb push_back
#define rep(i,x) for(int i=0;i<x;i++)
#define rep1(i,x) for(int i=1;i<=x;i++)
#define rrep(i,x) for(int i=x-1;i>=0;i--)
#define rrep1(i,x) for(int i=x;i>0;i--)
#define so(v) sort(v.begin(),v.end())
#define re(s) reverse(s.begin(),s.end())
#define lb(v,a) lower_bound(v.begin(),v.end(),a)
#define ub(v,a) upper_bound(v.begin(),v.end(),a)
#define mp1(a,b,c) piii(a,pii(b,c))
 
const int INF=1000000000;
const int dir_4[4][2]={{1,0},{0,1},{-1,0},{0,-1}};
const int dir_8[8][2]={{1,0},{1,1},{0,1},{-1,1},{-1,0},{-1,-1},{0,-1},{1,-1}};
const ll mod=1e9+7;

int a[10][10],b[10][10],c[10][10],sum=0;

int dfs(int k){
  int ret;
  if(k==9){
    ret=0;
    rep(i,2) rep(j,3) if(a[i+1][j]==a[i][j]) ret+=b[i][j];
    rep(i,3) rep(j,2) if(a[i][j+1]==a[i][j]) ret+=c[i][j];
    return ret;
  }
  if(k%2==0){
    ret=0;
    rep(i,3) 
      rep(j,3)
      if(a[i][j]==-1){
	a[i][j]=0;
	ret=max(ret,dfs(k+1));
	a[i][j]=-1;
      }
  }
  if(k%2){
    ret=10000;
    rep(i,3)
      rep(j,3)
      if(a[i][j]==-1){
	a[i][j]=1;
	ret=min(ret,dfs(k+1));
	a[i][j]=-1;
      }
  }
  return ret;
}

int main(){
  
  rep(i,3) rep(j,3) a[i][j]=-1;
  rep(i,2) rep(j,3){ cin>>b[i][j]; sum+=b[i][j];}
  rep(i,3) rep(j,2){ cin>>c[i][j]; sum+=c[i][j];}
 
  int ans=dfs(0);
  cout<<ans<<endl<<sum-ans<<endl;
  return 0;
}
