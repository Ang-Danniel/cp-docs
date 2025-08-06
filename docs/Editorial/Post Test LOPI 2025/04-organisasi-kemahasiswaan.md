# Organisasi Kemahasiswaan

**Link Soal:** [Gemastik Final 2017 - Problem A](link-soal-disini)  
**Sumber:** Gemastik Final 2017 / TLX
**Tingkat Kesulitan:** Medium
**Tag:** Math, Number Theory

## Overview Permasalahan

Terdapat N organisasi kemahasiswaan di Fasilkom UI. Organisasi ke-i terdiri atas tepat M[i] mahasiswa. Menurut peraturan fakultas, setiap mahasiswa hanya boleh tergabung pada paling banyak K organisasi.

Berapakah banyaknya mahasiswa Fasilkom UI paling sedikit yang mungkin?

## Hints

??? info "Hint 1"
    
    Banyak mahasiswa minimum adalah M[i] paling maksimum.


??? info "Hint 2"
    
    Buatlah tabel dimana mahasiswa merepresentasikan kolom dan baris merepresentasikan organisasi mahasiswa kolom i ikuti.

## Solusi

??? success "Solusi"
    
    P
    Perhatikan jika banyak mahasiswa adalah sebanyak T maka persamaan T * K >= Sumasi(M[i]) haruslah terpenuhi. T juga harus >= M[i] paling maksimum.

    Menurut PHP, hanya ketika T * K < Sumasi(M[i]) terdapat mahasiswa yang mengikuti lebih dari K organisasi. Untuk memudahkan visualisasi kamu dapat mengganggap T * K adalah sebuah tabel dimana mahasiswa merepresentasikan kolom dan baris merepresentasikan organisasi mahasiswa kolom i ikuti.

    Bila masukan:
    ```
    1
    7 4
    2 3 4 5 6 7 8
    ```

    Contoh tabel distribusi mahasiswa ke organisasi (misal T = 8, K = 4, M = [3, 3, 4, 5, 6, 7, 8]):

    | Organisasi | Mahasiswa ke-1 | Mahasiswa ke-2 | Mahasiswa ke-3 | Mahasiswa ke-4 | Mahasiswa ke-5 | Mahasiswa ke-6 | Mahasiswa ke-7 | Mahasiswa ke-8 | Mahasiswa ke-9 |
    |------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|
    | Org ke-1   | 7              | 7              | 7              | 7              | 7              | 7              | 7              | 7              | 6              |
    | Org ke-2   | 6              | 6              | 6              | 6              | 6              | 6              | 5              | 5              | 5              |
    | Org ke-3   | 5              | 5              | 5              | 4              | 4              | 4              | 4              | 4              | 4              |
    | Org ke-4   | 3              | 3              | 3              | 3              | 2              | 2              | 2              | 1              | 1              |


    Dapat dilihat bahwa tidak ada mahasiswa yang organisasi nya overlap karena banyak kolom lebih dari M[i] paling maksimum. Jadi kita cukup mencari nilai T dimana T = ceil(Sumasi(M[i]) / K) dan T harus lebih besar dari M[i] paling maksimum.

    - **Time Complexity:** O(1)
    - **Space Complexity:** O(1)

### Implementasi

??? example "Implementasi"

    ```cpp title="Solution" linenums="8"
    ll n, k; cin >> n >> k;
    
    ll sum = 0;
    ll maxx = 0;
    for (int i = 0; i < n; i++){
        ll temp; cin >> temp;
        sum += temp;
        maxx = max(maxx, temp);
    }

    ll ans = (sum / k);
    if (sum % k != 0) ans++;
    ans = max(maxx, ans);
    cout << ans << endl;
    ```