# Variasi Umum BFS dan DFS

Setelah memahami algoritma dasar BFS dan DFS, penting untuk menguasai berbagai variasi yang sering digunakan dalam pemrograman kompetitif. Variasi-variasi ini sangat berguna untuk menyelesaikan masalah graf yang lebih kompleks seperti pengecekan konektivitas, deteksi siklus, pencarian jalur terpendek, dan rekonstruksi jalur.

### Pengenalan Variasi
Algoritma BFS dan DFS memiliki banyak aplikasi praktis yang merupakan modifikasi dari implementasi dasar. Variasi-variasi ini memungkinkan kita untuk:

- Menganalisis struktur graf (connected components, cycles)
- Mencari jalur optimal (shortest path, path finding)
- Melakukan operasi dari multiple sources secara bersamaan
- Merekonstruksi jalur yang telah ditemukan

Mari kita bahas setiap variasi dengan implementasi dan contoh penggunaannya.

## Connected Components

### Masalah

Connected component adalah kelompok vertex dalam graf di mana setiap vertex dapat dijangkau dari vertex lain dalam kelompok yang sama. Menentukan jumlah dan isi dari setiap connected component penting untuk analisis connectivity graf.

**Input:**  
- `n` = jumlah vertex  
- `m` = jumlah edge  
- Diikuti `m` baris pasangan edge: `u v`

**Output:**  
- Jumlah connected components  
- Daftar vertex pada setiap component

**Contoh Input:**
```
6 4
1 2
2 3
4 5
5 6
```

**Contoh Output:**
```
Jumlah connected components: 2
```

### Penyelesaian

Gunakan DFS untuk menandai setiap vertex yang sudah dikunjungi dan mengelompokkan vertex ke dalam komponen yang sama.

```cpp title="Connected Components dengan DFS" linenums="1"
#include <iostream>
#include <vector>
#include <cstring>
using namespace std;

const int MAXN = 100005;
vector<int> adj[MAXN];
bool visited[MAXN];
int n, m;

// DFS untuk mengumpulkan vertex dalam satu komponen
void dfs(int u, vector<int>& component) {
    visited[u] = true;
    for (int v : adj[u]) {
        if (!visited[v]) {
            dfs(v, component);
        }
    }
}

int main() {
    cin >> n >> m;
    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    memset(visited, false, sizeof(visited));
    int ans = 0;

    for (int i = 1; i <= n; i++) {
        if (!visited[i]) {
            dfs(i, component);
            ans++;
        }
    }

    cout << "Jumlah connected components: " << ans << endl;
    return 0;
}
```

### Kompleksitas Connected Components

| Aspek | Kompleksitas |
|-------|--------------|
| **Time Complexity** | O(V + E) |
| **Space Complexity** | O(V) |

## Cycle Detection dengan DFS (Directed Graph)

### Masalah

Diberikan sebuah directed graph, tentukan apakah terdapat cycle di dalamnya.

**Input:**  
- `n` = jumlah vertex  
- `m` = jumlah edge  
- Diikuti `m` baris pasangan edge: `u v`

**Output:**  
- "YES" jika terdapat cycle  
- "NO" jika tidak ada cycle

### Penyelesaian

Gunakan DFS dengan dua array:  
- `vis[]` untuk menandai node yang sudah dikunjungi  
- `pathDfs[]` untuk menandai node yang sedang ada di jalur DFS saat ini

Jika saat DFS menemukan node yang sudah ada di `pathDfs`, berarti terdapat cycle.

```cpp title="Cycle Detection - Directed Graph" linenums="1"
#include <iostream>
#include <vector>
using namespace std;

const int MAXN = 100005;
vector<int> adj[MAXN];
bool vis[MAXN], pathDfs[MAXN];
int n, m;
bool foundCycle = false;

bool dfs(int cur) {
    vis[cur] = true;
    pathDfs[cur] = true;

    for (auto v : adj[cur]) {
        if (pathDfs[v]) {
            return true; // Cycle detected
        }
        if (!vis[v]) {
            if (dfs(v)) return true;
        }
    }
    pathDfs[cur] = false;
    return false;
}

int main() {
    cin >> n >> m;
    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
    }

    for (int i = 1; i <= n; i++) {
        if (!vis[i]) {
            if (dfs(i)) {
                cout << "YES" << endl;
                return 0;
            }
        }
    }
    cout << "NO" << endl;
    return 0;
}
```

## Shortest Path dengan BFS

### Masalah

Diberikan sebuah unweighted graph dengan `n` vertex dan `m` edge, carilah jalur terpendek dari node `source` ke node `target`. Jika tidak ada jalur, keluarkan `-1`.

**Input:**  
- `n` = jumlah vertex  
- `m` = jumlah edge  
- Diikuti `m` baris pasangan edge: `u v`  
- `source` dan `target` (node awal dan tujuan)

**Output:**  
- Jarak terpendek dari `source` ke `target`, atau `-1` jika tidak ada jalur  
- Jalur yang dilalui (jika ada)

### Penyelesaian

Gunakan BFS untuk mencari shortest path pada unweighted graph. BFS menjamin jalur terpendek karena mengeksplorasi vertex berdasarkan jarak minimum dari source. Simpan parent setiap node untuk merekonstruksi jalur.

```cpp title="BFS Shortest Path" linenums="1"
#include <iostream>
#include <vector>
#include <queue>
#include <algorithm>
#include <climits>
using namespace std;

const int MAXN = 100005;
const int INF = INT_MAX;

vector<int> adj[MAXN];
int dist[MAXN];
int parent[MAXN];

int main() {
    int n, m, source, target;
    cin >> n >> m >> source >> target;

    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    for (int i = 0; i < MAXN; i++) {
        dist[i] = INF;
        parent[i] = -1;
    }

    queue<int> q;
    dist[source] = 0;
    q.push(source);

    while (!q.empty()) {
        int u = q.front();
        q.pop();

        for (int v : adj[u]) {
            if (dist[v] == INF) {
                dist[v] = dist[u] + 1;
                parent[v] = u;
                q.push(v);
            }
        }
    }

    if (dist[target] == INF) {
        cout << -1 << endl;
    } else {
        cout << "Shortest distance: " << dist[target] << endl;
        vector<int> path;
        int cur = target;
        while (cur != -1) {
            path.push_back(cur);
            cur = parent[cur];
        }
        reverse(path.begin(), path.end());
        cout << "Path: ";
        for (int i = 0; i < path.size(); i++) {
            if (i > 0) cout << " -> ";
            cout << path[i];
        }
        cout << endl;
    }

    return 0;
}
```
### Kompleksitas Shortest Path BFS

| Aspek | Kompleksitas |
|-------|--------------|
| **Time Complexity** | O(V + E) |
| **Space Complexity** | O(V) |

## Multi Source BFS

Multi Source BFS adalah teknik pencarian jalur terpendek dari beberapa titik awal (source) sekaligus dalam sebuah graf.

#### Cara Kerja

Pada Multi Source BFS, semua node sumber dimasukkan ke dalam queue pada awal proses. BFS kemudian berjalan seperti biasa, namun setiap node yang dikunjungi akan memiliki jarak minimum dari salah satu sumber. Dengan cara ini, kita dapat menghitung jarak terdekat dari semua sumber ke setiap node di graf.

#### Implementasi Dasar

```cpp title="Multi Source BFS" linenums="1"
#include <iostream>
#include <vector>
#include <queue>
#include <climits>
using namespace std;

const int MAXN = 100005;
const int INF = INT_MAX;

vector<int> adj[MAXN];
int dist[MAXN];

int main() {
    int n, m, k;
    cin >> n >> m >> k;
    vector<int> sources(k);
    for (int i = 0; i < k; i++) {
        cin >> sources[i];
    }
    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    for (int i = 0; i < MAXN; i++) dist[i] = INF;
    queue<int> q;
    for (int src : sources) {
        dist[src] = 0;
        q.push(src);
    }
    while (!q.empty()) {
        int u = q.front(); q.pop();
        for (int v : adj[u]) {
            if (dist[v] == INF) {
                dist[v] = dist[u] + 1;
                q.push(v);
            }
        }
    }
    for (int i = 1; i <= n; i++) {
        cout << "Node " << i << ": " << dist[i] << endl;
    }
    return 0;
}
```

#### Kompleksitas Multi Source BFS

| Aspek | Kompleksitas |
|-------|--------------|
| **Time Complexity** | O(V + E) |
| **Space Complexity** | O(V) |

#### Contoh Soal Klasik

- [CSES Monsters](https://cses.fi/problemset/task/1194)

## Shortest Path dengan Path nya

Seringkali dalam pemrograman kompetitif, kita tidak hanya perlu mengetahui jarak terpendek tetapi juga jalur yang dilalui untuk mencapai tujuan tersebut. Teknik ini menggunakan konsep **parent tracking** untuk merekonstruksi jalur setelah BFS selesai.

### Cara Kerja

1. **Simpan Parent**: Saat melakukan BFS, simpan informasi parent dari setiap vertex yang dikunjungi
2. **Backtrack**: Setelah mencapai target, ikuti parent chain dari target kembali ke source
3. **Reverse**: Karena kita backtrack dari target ke source, reverse hasil untuk mendapatkan jalur yang benar

### Implementasi Dasar

```cpp title="BFS dengan Path Reconstruction" linenums="1"
#include <iostream>
#include <vector>
#include <queue>
#include <algorithm>
#include <climits>
using namespace std;

const int MAXN = 100005;
const int INF = INT_MAX;

vector<int> adj[MAXN];
int dist[MAXN];
int parent[MAXN];

int main() {
    int n, m, source, target;
    cin >> n >> m >> source >> target;
    
    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    
    // Initialize
    for (int i = 1; i <= n; i++) {
        dist[i] = INF;
        parent[i] = -1;
    }
    
    queue<int> q;
    dist[source] = 0;
    q.push(source);
    
    while (!q.empty()) {
        int u = q.front();
        q.pop();
        
        // Early termination jika target sudah ditemukan
        if (u == target) break;
        
        for (int v : adj[u]) {
            if (dist[v] == INF) {
                dist[v] = dist[u] + 1;
                parent[v] = u;  // Simpan parent
                q.push(v);
            }
        }
    }
    
    if (dist[target] == INF) {
        cout << "No path exists" << endl;
    } else {
        cout << "Shortest distance: " << dist[target] << endl;
        
        // Reconstruct path
        vector<int> path;
        int current = target;
        while (current != -1) {
            path.push_back(current);
            current = parent[current];
        }
        
        reverse(path.begin(), path.end());
        
        cout << "Path: ";
        for (int i = 0; i < path.size(); i++) {
            if (i > 0) cout << " -> ";
            cout << path[i];
        }
        cout << endl;
    }
    
    return 0;
}
```

**Contoh Input:**
```
5 5 1 5
1 2
2 3
3 5
1 4
4 5
```

**Contoh Output:**
```
Shortest distance: 3
Path: 1 -> 4 -> 5
```

### Kompleksitas Shortest Path dengan Path

| Aspek | Kompleksitas |
|-------|--------------|
| **Time Complexity** | O(V + E) |
| **Space Complexity** | O(V) |
| **Path Reconstruction** | O(path_length) |

### Contoh Soal Klasik

- [Message Route](https://cses.fi/problemset/task/1667)

## Kesimpulan

Sebenarnya masih banyak yang dapat dibahas disini karena variasi graph cukup banyak dan tidak semua penulis kuasai, web ini akan diupdate jika saya niat hihi.