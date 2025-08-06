# X-Emas

**Link Soal:** [X-Emas - Problem E](https://tlx.toki.id/problems/troc-40/E/)  
**Sumber:** TROC / TLX
**Tingkat Kesulitan:** Hard  
**Tag:** Binary Search, Prefix Sum

## Solusi

??? success "Solusi"
    
    Pertama-tama, kita dapat mengurutkan tambang berdasarkan nilai Ai terbesar hingga terkecil. Untuk kegiatan menambang, kita hanya perlu memperhatikan tambang dengan nilai terbesar (Amax) dan terbesar kedua (Amax2). Sementara itu, untuk kegiatan mengebom, kita hanya perlu memperhatikan tambang yang memiliki nilai 2Ai >= Amax2.

    Perhatikan bahwa urutan kegiatan menambang dan mengebom tambang emas tidaklah penting, karena di akhir kita dapat mengatur urutan kegiatan supaya memenuhi aturan. Kondisi yang perlu diperhatikan agar urutan kegiatan menambang dan mengebom memenuhi aturan adalah banyaknya penambangan Amax harus tidak lebih dari banyaknya pengeboman ditambah banyaknya penambangan Amax2.

    Untuk mendapatkan emas semaksimal mungkin, kita dapat memprioritaskan kegiatan menambang dan mengebom dengan urutan sebagai berikut:

    1. Mengebom seluruh tambang yang memiliki nilai 2Ai >= Amax.
    2. Menambang tambang Amax sebanyak kegiatan mengebom yang dilakukan sebelumnya.
    3. Mengebom seluruh tambang yang memiliki nilai Amax > 2Ai >= Amax2, diselingi dengan menambang tambang Amax. Hati-hati: kegiatan mengebom harus didahulukan agar urutan kegiatan tetap memenuhi aturan.
    4. Menambang tambang Amax2 diselingi menambang tambang Amax. Hati-hati: kegiatan menambang tambang Amax2 harus didahulukan, dengan alasan yang sama seperti sebelumnya. Perhatikan juga kemungkinan overflow jika jumlah emas dihitung secara manual.

    Menentukan banyaknya hari minimum yang dibutuhkan untuk mendapatkan setidaknya X kilogram emas dapat dilakukan menggunakan binary search the answer (BSTA).

    Kompleksitas waktu: O(N(log N + log X)).

    Terdapat pula solusi tanpa BSTA yang bekerja dalam O(N log N).

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

    int main(){
        semoga_ac;
        int n; cin >> n;
        ll x; cin >> x;

        ll ar[n + 1];
        vector<ll> prefBest;
        for(int i = 0; i <= n; i++) {
            cin >> ar[i]; 
        }
        
        sort(ar, ar + n);

        ll best1 = ar[n - 1];
        ll best2 = ar[n - 2];

        ll sum = 0;
        for (int i = n - 1; i >= 0; i--) {
            ll twoTimes = 2ll * ar[i];
            if (twoTimes >= best1) {
                sum += twoTimes;
                prefBest.pb(sum);
            } else {
                for(int j = n - 1; j > i; j--) {
                    sum += best1;
                    prefBest.pb(sum);
                }
                for (int j = i; j >= 0; j--) {
                    twoTimes = 2ll * ar[j];
                    if (twoTimes >= best2) {
                        sum += twoTimes;
                        prefBest.pb(sum);
                        sum += best1;
                        prefBest.pb(sum);
                    } else {
                        break;
                    }
                }
                break;
            }

            if (i == 0) {
                for(int j = n - 1; j > i; j--) {
                    sum += best1;
                    prefBest.pb(sum);
                }
            }
        }

        ll m = prefBest.size();
        ll ans = 0;
        if (prefBest[m - 1] < x) {
            x -= prefBest[m - 1];
            ll sumBest = best1 + best2;
            ans = m + (x / sumBest) * 2ll;
            if (x % sumBest <= best2) {
                ans++;
            } else if (x % sumBest > best2) {
                ans+=2;
            }
        } else {
            int l, r, mid;
            l = 0;
            r = m - 1;
            while (l <= r) {
                mid = (l + r) / 2;
                if(prefBest[mid] >= x) {
                    ans = mid + 1;
                    r = mid - 1;
                } else {
                    l = mid + 1;
                }
            }
        }

        // for(int i = 0; i < m; i++) cout << prefBest[i] << " ";
        // cout << endl;
        cout << ans << endl;
    }   
    ```