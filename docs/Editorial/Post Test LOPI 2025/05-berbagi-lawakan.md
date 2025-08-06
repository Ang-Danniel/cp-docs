# Berbagi Lawakan

**Link Soal:** [Gemastik 17 - Problem I](https://tlx.toki.id/problems/gemastik-2017-pemrograman-final/I)  
**Sumber:** Contest Name / Platform Name  
**Tingkat Kesulitan:** Easy/Medium/Hard  
**Tag:** Graph, BFS, Implementation, etc.

## Overview Permasalahan

Jelaskan permasalahan secara singkat dan jelas. Apa yang diminta dalam soal? Apa input dan output yang diharapkan?

Contoh:
- Input: Deskripsi format input
- Output: Deskripsi format output
- Constraints: Batasan-batasan yang diberikan

## Hints

??? info "Hint 1"
    
    Sebuah lawakan abadi bila terdapat siklus yang terdiri dari pelawak-pelawak yang menyukai lawakan tersebut.

??? info "Hint 2"

    Untuk mencari sebuah siklus, Anda dapat menggunakan DFS seperti pada [artikel berikut](../../Topik Umum/Graf Dasar/03-variasi-umum.md) (Cycle Detection).    
   
## Solusi

??? success "Solusi"

    Untuk menentukan apakah sebuah lawakan dapat menjadi abadi, kita perlu mencari apakah terdapat jalur menuju sebuah siklus yang terdiri dari pelawak-pelawak yang menyukai lawakan tersebut. Hal ini dapat dilakukan dengan melakukan DFS yang dimulai dari suatu node dan membentuk path menuju node lain. Jika node berikutnya yang akan dikunjungi sudah terdapat dalam path DFS saat ini, maka seluruh node pada path tersebut dapat dianggap mampu membuat lawakan yang dimulai dari node tersebut menjadi abadi.

    Namun ini saja tidak cukup, kita perlu mengoptimasi setiap pertanyaan yang diberikan dimana kita dapat menggunakan array sebesar 100 × 50000 untuk menampung informasi dari tiap node, atau memproses seluruh pertanyaan dari yang nilai humornya paling rendah ke paling besar.

    - **Time Complexity:** O(M + N + Q)
    - **Space Complexity:** O(M + N)

### Implementasi

??? example "Implementasi"

    ```cpp title="Solution" linenums="1"
    #include <iostream>
    #include <vector>
    #include <string>
    #include <algorithm>
    #include <cmath>
    #include <map>
    #include <set>
    #include <stack>
    #include <queue>
    #include <deque>
    #include <bitset>
    #include <iomanip>
    #include <complex>
    #include <numeric>
    #include <climits>
    #include <cassert>
    #include <cstring>
    #include <chrono>
    #include <random>

    typedef long long ll;
    typedef unsigned long long ull;
    #define pb push_back
    #define eb emplace_back
    #define ppb pop_back
    #define fi first
    #define se second
    #define ub upper_bound
    #define lb lower_bound
    #define pii pair<int,int>
    #define pll pair<ll,ll>
    #define rep(i,n) for (i = 0; i < n; ++i)
    #define REP(i,k,n) for (i = k; i <= n; ++i)
    #define REPR(i,k,n) for (i = k; i >= n; --i)
    using namespace std;
    const ll MOD = 1e9 + 7;
    #define semoga_ac ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)

    typedef complex<double> P;
    #define X real()
    #define Y imag()
    typedef vector<int> vi;
    typedef vector<vi> vvi;

    int a[50001];
    int b[50001];

    vector<int> adj[50001];
    bool ans[101][50001];
    bool vis[50001];

    bool temp[50001];

    void dfs(int cur, int h) {
        vis[cur] = true;

        if (!((a[cur] <= h) && (b[cur] >= h))){
            return;
        }

        temp[cur] = true;

        for (auto v: adj[cur]) {
            if (temp[v] && (a[v] <= h) && (b[v] >= h)) {
                ans[h][cur] = true;
            }

            if(!vis[v] && (a[v] <= h) && (b[v] >= h)) {
                dfs(v, h);
            }

            if (ans[h][v] && (a[v] <= h) && (b[v] >= h)) {
                ans[h][cur] = true;
            }
        }
        temp[cur] = false;
    }

    int main(){
    semoga_ac;
        int n, m; cin >> n >> m; 
        
        for (int i = 1; i <= n; i++) {
            cin >> a[i];
        }
        for (int i = 1; i <= n; i++) {
            cin >> b[i];
        }

        int u, v; 
        for (int i = 1; i <= m; i++) {
            cin >> u >> v;
            adj[u].pb(v);
        }

        for (int i = 0; i <= 100; i++) {
            memset(vis, false, sizeof(vis));
            for (int j = 1; j <= n; j++) {
                if (!vis[j]) dfs(j, i);
            }
        }

        int q; cin >> q;
        for (int i = 0; i < q; i++) {
            cin >> u >> v;
            if(ans[v][u]) cout << "Ya" << endl;
            else cout << "Tidak" << endl; 
        }
    }
    ```

