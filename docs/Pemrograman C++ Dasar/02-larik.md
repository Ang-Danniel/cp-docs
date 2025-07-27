# Larik (Array)
Larik atau *array* merupakan struktur data fundamental yang sangat penting dalam pemrograman dan akan **muncul** di berbagai soal kompetitif, mulai dari penyimpanan data, pencarian, pengurutan, hingga algoritma dinamis. Dengan memahami array, kita dapat menyimpan dan mengolah banyak data dengan efisien tanpa membuat variabel berulang-ulang.

### Pengenalan
Mari kita mulai dengan contoh permasalahan sederhana:

> Simpan dan cetak nilai dari 5 siswa.

Jika kita menulis:
```cpp linenums="1"
int nilai1, nilai2, nilai3, nilai4, nilai5;
cin >> nilai1 >> nilai2 >> nilai3 >> nilai4 >> nilai5;
cout << nilai1 << " " << nilai2 << " " << nilai3 << " " << nilai4 << " " << nilai5;
```
Maka jelas, ini tidak efisien. Di sinilah array dibutuhkan: kita bisa menyimpan banyak data dalam satu variabel dengan indeks yang berbeda.

### Deklarasi Array
Array adalah kumpulan elemen dengan tipe data yang sama, disimpan dalam lokasi memori yang berurutan.

```cpp title="Struktur Umum" linenums="1"
tipe_data nama_array[ukuran];
```

```cpp title="Contoh Deklarasi" linenums="1"
int nilai[5];           // Array integer dengan 5 elemen
char huruf[10];         // Array karakter dengan 10 elemen
double harga[100];      // Array double dengan 100 elemen
```

Kegunaan umum di pemrograman kompetitif:

- Menyimpan input data dalam jumlah besar
- Implementasi algoritma pencarian dan pengurutan
- Dynamic Programming
- Manipulasi string (array of char)

### Indeks Array
Array menggunakan sistem indeks yang dimulai dari 0. Untuk array dengan ukuran n, indeksnya adalah 0, 1, 2, ..., n-1.

| Indeks      | nilai[0] | nilai[1] | nilai[2] | nilai[3] | nilai[4] |
| ----------- | -------- | -------- | -------- | -------- | -------- |
| **Nilai**   |   10     |   20     |   30     |   40     |   50     |

```cpp title="Mengakses Elemen Array" linenums="1"
int nilai[5];
nilai[0] = 10;  // Elemen pertama
nilai[1] = 20;  // Elemen kedua
nilai[2] = 30;  // Elemen ketiga
nilai[3] = 40;  // Elemen keempat
nilai[4] = 50;  // Elemen kelima

cout << nilai[0] << endl;  // Output: 10
cout << nilai[2] << endl;  // Output: 30
```

!!! warning "Index Out of Bounds"
    Pastikan indeks yang diakses tidak melebihi ukuran array. Mengakses `nilai[5]` pada array dengan ukuran 5 akan menyebabkan error atau perilaku tidak terduga.

### Inisialisasi Array
Ada beberapa cara untuk menginisialisasi array:

```cpp title="Inisialisasi Langsung" linenums="1"
int angka[5] = {1, 2, 3, 4, 5};
// angka[0] = 1, angka[1] = 2, dst.
```

```cpp title="Inisialisasi Sebagian" linenums="1"
int angka[5] = {1, 2};  // Sisa elemen otomatis 0
// angka[0] = 1, angka[1] = 2, angka[2] = 0, angka[3] = 0, angka[4] = 0
```

```cpp title="Inisialisasi Semua Nol" linenums="1"
int angka[5] = {0};  // Semua elemen = 0
// atau
int angka[5] = {};   // Semua elemen = 0
```

```cpp title="Auto-sizing" linenums="1"
int angka[] = {1, 2, 3, 4, 5};  // Ukuran otomatis = 5
```

### Input dan Output Array
Penggunaan perulangan sangat penting untuk mengisi dan menampilkan array:

```cpp title="Input Array" linenums="1"
int n = 5;
int nilai[5];

// Mengisi array
for (int i = 0; i < n; i++) {
    cin >> nilai[i];
}
```

```cpp title="Output Array" linenums="1"
// Menampilkan array
for (int i = 0; i < n; i++) {
    cout << nilai[i] << " ";
}
cout << endl;
```

```cpp title="Contoh Lengkap" linenums="1"
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Masukkan jumlah elemen: ";
    cin >> n;
    
    int arr[100];  // Maksimal 100 elemen
    
    cout << "Masukkan " << n << " angka: ";
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }
    
    cout << "Array yang dimasukkan: ";
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
    
    return 0;
}
```

### Operasi Dasar Array

#### Mencari Elemen
```cpp title="Linear Search" linenums="1"
int cari = 30;
bool found = false;
int posisi = -1;

for (int i = 0; i < n; i++) {
    if (arr[i] == cari) {
        found = true;
        posisi = i;
        break;
    }
}

if (found) {
    cout << "Elemen " << cari << " ditemukan di indeks " << posisi << endl;
} else {
    cout << "Elemen tidak ditemukan" << endl;
}
```

#### Mencari Nilai Maksimum dan Minimum
```cpp title="Mencari Max dan Min" linenums="1"
int maksimum = arr[0];
int minimum = arr[0];

for (int i = 1; i < n; i++) {
    if (arr[i] > maksimum) {
        maksimum = arr[i];
    }
    if (arr[i] < minimum) {
        minimum = arr[i];
    }
}

cout << "Nilai maksimum: " << maksimum << endl;
cout << "Nilai minimum: " << minimum << endl;
```

#### Menghitung Jumlah dan Rata-rata
```cpp title="Sum dan Average" linenums="1"
int jumlah = 0;
for (int i = 0; i < n; i++) {
    jumlah += arr[i];
}

double rata_rata = (double)jumlah / n;
cout << "Jumlah: " << jumlah << endl;
cout << "Rata-rata: " << rata_rata << endl;
```

### Array 2 Dimensi (Matriks)
Array 2 dimensi berguna untuk menyimpan data dalam bentuk tabel atau matriks:

```cpp title="Deklarasi Array 2D" linenums="1"
int matriks[3][4];  // 3 baris, 4 kolom
// atau dengan inisialisasi
int matriks[3][4] = {
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 10, 11, 12}
};
```

```cpp title="Input dan Output Array 2D" linenums="1"
int baris = 3, kolom = 4;
int matriks[3][4];

// Input
cout << "Masukkan elemen matriks 3x4:" << endl;
for (int i = 0; i < baris; i++) {
    for (int j = 0; j < kolom; j++) {
        cin >> matriks[i][j];
    }
}

// Output
cout << "Matriks:" << endl;
for (int i = 0; i < baris; i++) {
    for (int j = 0; j < kolom; j++) {
        cout << matriks[i][j] << " ";
    }
    cout << endl;
}
```

### Visualisasi Array 2D
|         | **0**           | **1**           | **2**           | **3**           |
| ------- | --------------- | --------------- | --------------- | --------------- |
| **0**   | matriks[0][0]<br>1  | matriks[0][1]<br>2  | matriks[0][2]<br>3  | matriks[0][3]<br>4  |
| **1**   | matriks[1][0]<br>5  | matriks[1][1]<br>6  | matriks[1][2]<br>7  | matriks[1][3]<br>8  |
| **2**   | matriks[2][0]<br>9  | matriks[2][1]<br>10 | matriks[2][2]<br>11 | matriks[2][3]<br>12 |

### String sebagai Array Karakter
String dalam C++ dapat direpresentasikan sebagai array karakter:

```cpp title="Array Karakter" linenums="1"
char nama[50];
cout << "Masukkan nama: ";
cin >> nama;  // atau getline(cin, nama) untuk string dengan spasi
cout << "Halo, " << nama << endl;

// Mengakses karakter individual
cout << "Huruf pertama: " << nama[0] << endl;
```

```cpp title="Manipulasi String" linenums="1"
char kata[20] = "Hello";
int panjang = 0;

// Menghitung panjang string
while (kata[panjang] != '\0') {
    panjang++;
}
cout << "Panjang kata: " << panjang << endl;
```

### Tips dan Catatan Penting

!!! notes "Ukuran Array"
    Ukuran array harus dideklarasikan dengan konstanta atau literal. Anda tidak bisa menggunakan variabel untuk ukuran array dalam deklarasi standar C++.
    ```cpp
    int n = 5;
    int arr[n];  // Error di beberapa compiler
    
    // Gunakan konstanta
    const int UKURAN = 5;
    int arr[UKURAN];  // Benar
    ```

!!! warning "Bounds Checking"
    C++ tidak melakukan pengecekan batas array secara otomatis. Pastikan selalu menggunakan indeks yang valid:
    ```cpp
    int arr[5];
    arr[10] = 100;  // Berbahaya! Dapat menyebabkan crash
    ```

!!! tip "Inisialisasi Awal"
    Selalu inisialisasi array sebelum digunakan untuk menghindari nilai sampah:
    ```cpp
    int arr[100] = {0};  // Semua elemen diisi 0
    ```

### Kesimpulan
Array adalah struktur data fundamental yang memungkinkan kita menyimpan dan mengolah banyak data dengan tipe yang sama secara efisien. Konsep indeks yang dimulai dari 0, operasi input/output menggunakan perulangan, dan berbagai algoritma dasar seperti pencarian dan pengurutan adalah skill penting yang harus dikuasai.

Array 2 dimensi berguna untuk representasi data tabular dan matriks, sementara array karakter dapat digunakan untuk manipulasi string dasar. Memahami array dengan baik akan menjadi fondasi untuk mempelajari struktur data yang lebih kompleks seperti vector, stack, queue, dan algoritma yang lebih advanced.

Praktik yang konsisten dengan berbagai operasi array akan membantu Anda menguasai konsep ini dengan baik. Array sangat sering muncul dalam soal pemrograman kompetitif, jadi pastikan Anda memahami semua konsep dasar yang telah dijelaskan.

### Contoh Soal TLX

- [Kandang Terbesar](https://tlx.toki.id/courses/basic-cpp/chapters/06/problems/C)
- [Jual Beli Bebek III](https://tlx.toki.id/courses/basic-cpp/chapters/06/problems/D)
- [Bermain Lampu Kandang](https://tlx.toki.id/courses/basic-cpp/chapters/06/problems/E)
- [Toko Kandang II](https://tlx.toki.id/courses/basic-cpp/chapters/06/problems/F)
- [Menutup Toko](https://tlx.toki.id/courses/basic-cpp/chapters/06/problems/G)