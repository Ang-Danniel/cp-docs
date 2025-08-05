# Plus Minus

**Link Soal:** [TLX TOC 2017 OCT 2B]()  
**Sumber:** TOC 2017 / TLX
**Tingkat Kesulitan:** Easy
**Tag:** Math/DP

## Overview Permasalahan

Diberikan persamaan _ 1 _ 2 _ ... N-1 = N. Kita perlu menentukan apakah ada kemungkinan tertentu sehingga persamaan tersebut valid. 

N hanya berkisar dari 1 hingga 100 (inklusif).

## Hints

??? info "Hint 1"
    
    Buatlah hasil untuk N = 1 hingga N = 8. Lakukan percobaan.

??? info "Hint 2"
    
    Asumsikan semua operatornya + terlebih dahulu kemudian sesuaikan.

## Solusi

??? success "Solusi"
    
    Mari kita gunakan contoh ketika N = 4 dan asumsikan bahwa seluruh operator adalah plus.
    Maka total persamaan kiri adalah `3 (4) / 2 = 6`, Bila kita mengubah suatu tanda dari salah satu operator yang ada maka total persamaan kiri akan berkurang sebanyak 2 kali dari bilangan yang dirubah ke negatif.

    Sebagai contoh
    + 1 + 2 + 3 = 6
    Bila kita mengubah + 1 menjadi - 1 maka
    - 1 + 2 + 3 = 4
    Atau dalam kata lain berkurang sebanyak 2 * 1 (dimana 1 adalah bilangan yang diubah ke negatif)

    Kesimpulannya adalah kita dapat mengurangi sebanyak bilangan genap saja. Sehingga bila kedua (N * (N - 1) / 2) dan N tidak ganjil atau genap, maka tidak mungkin untuk membuat persamaan tersebut!

    Sementara jika keduanya genap atau ganjil, kita dapat selalu pasti menemukan suatu kombinasi pengurangan sehingga kita menjelajahi setiap kemungkinan ganjil dan genap yang mungkin.

    Misal pada contoh N = 4
    + 1 + 2 + 3 = 6
    - 1 + 2 + 3 = 4
    + 1 - 2 + 3 = 2
    + 1 + 2 - 3 = 0
    dst

    - **Time Complexity:** O(1)
    - **Space Complexity:** O(1)

### Implementasi

??? example "Implementasi"

    ```cpp title="Solution" linenums="1"
    int n; cin >> n;
    if (n % 4 == 1) cout << "TIDAK";
    else if (n % 4 == 2) cout << "TIDAK";
    else cout << "YA";
    ```
:3
