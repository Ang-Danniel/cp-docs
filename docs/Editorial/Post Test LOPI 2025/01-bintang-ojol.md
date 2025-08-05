# Bintang Ojol

**Link Soal:** [Penyisihan CPC Senior - Bintang Ojol](https://tlx.toki.id/problems/compfest-12-scpc-penyisihan/B/)  
**Sumber:** Penyisihan CPC Senior / TLX
**Tingkat Kesulitan:** Easy  
**Tag:** Greedy, Math

## Overview Permasalahan

Diberikan N dan M sebagai input dimana N adalah banyak bintang total yang akan di distribusikan ke M Ojol. Tentukan banyak Ojol maksimum dan minimum yang menerima bintang 5!

## Hints

??? info "Hint 1"
    
    Perhatikan constraint yang diberikan, sudah tidak mungkin untuk membuat solusi dalam linear time!

??? info "Hint 2"
    
    Jika anda ingin meminimumkan banyak ojol berbintang 5 maka anda harus membuang bintang sebanyak mungkin.

## Solusi

??? success "Solusi"
    
    Perhatikan jika kita ingin memaksimalkan banyak ojol berbintang 5, kita dapat mengawali seluruh ojol dengan bintang 1 kemudian membagi rata bintang 4 yang ada dengan pembagian biasa.  

    `jawaban = (banyak_bintang - banyak_ojol) / 4;`

    Sementara untuk meminimalkan, kita dapat membuat semua ojol berbintang 4 dan kemudian mendistribusikan bitang 1 yang tersisa.

    `jawaban = banyak_ojol - (banyak_bintang / 4);`

    - **Time Complexity:** O(1)
    - **Space Complexity:** O(1)

### Implementasi

??? example "Implementasi"

    ```cpp title="Solution" linenums="1"
    ll n, m; cin >> n >> m;
    ll minn, maxx;
    minn = maxx = -1;
    
    if(!(m * 5ll < n || n < m)){ // Cek apakah bintang tidak dapat atau melebihi dari yang bisa didistribusikan
        ll nt;
        nt = n;
        nt -= m;
        maxx = nt / 4ll; 

        if(n <= 4ll * m){
            minn = 0;
        }else{
            minn = n - (4ll * m);
        }
    }
    cout << minn << " " << maxx;
    ```

:3
