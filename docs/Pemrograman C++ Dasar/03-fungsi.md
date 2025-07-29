# Fungsi
Fungsi merupakan blok kode yang dapat dipanggil berulang kali untuk melakukan tugas tertentu, mulai dari modularisasi kode, implementasi algoritma, hingga penggunaan library functions. Dengan memahami fungsi, kita dapat menulis kode yang lebih terorganisir, mudah dibaca, dan dapat digunakan kembali.

### Pengenalan
Mari kita mulai dengan contoh permasalahan sederhana:

> Hitung luas persegi panjang untuk beberapa pasang panjang dan lebar yang berbeda.

Jika kita menulis:
```cpp linenums="1"
int panjang1 = 5, lebar1 = 3;
int luas1 = panjang1 * lebar1;
cout << "Luas 1: " << luas1 << endl;

int panjang2 = 7, lebar2 = 4;
int luas2 = panjang2 * lebar2;
cout << "Luas 2: " << luas2 << endl;
// ... dan seterusnya
```
Maka jelas, ini tidak efisien. Di sinilah fungsi dibutuhkan: kita bisa membuat satu blok kode yang dapat dipanggil berulang kali dengan parameter yang berbeda.

### Deklarasi dan Definisi Fungsi
Fungsi adalah blok kode yang menerima input (parameter), melakukan pemrosesan, dan dapat mengembalikan output (return value).

```cpp title="Struktur Umum" linenums="1"
tipe_return nama_fungsi(parameter1, parameter2, ...) {
    // blok kode
    return nilai; // opsional
}
```

```cpp title="Contoh Fungsi Sederhana" linenums="1"
// Fungsi menghitung luas persegi panjang
int hitungLuas(int panjang, int lebar) {
    int luas = panjang * lebar;
    return luas;
}

// Fungsi tanpa return value (void)
void cetakPesan(string pesan) {
    cout << "Pesan: " << pesan << endl;
}
```

Kegunaan umum di pemrograman kompetitif:

- Modularisasi kode untuk menghindari repetisi
- Implementasi algoritma khusus (sorting, searching)
- Validasi input dan output
- Penggunaan library functions untuk efisiensi

### Memanggil Fungsi
Setelah fungsi didefinisikan, kita dapat memanggilnya di dalam program:

```cpp title="Pemanggilan Fungsi" linenums="1"
#include <iostream>
using namespace std;

// Definisi fungsi
int hitungLuas(int panjang, int lebar) {
    return panjang * lebar;
}

void cetakPesan(string pesan) {
    cout << "Pesan: " << pesan << endl;
}

int main() {
    // Memanggil fungsi dengan return value
    int hasil = hitungLuas(5, 3);
    cout << "Luas: " << hasil << endl;
    
    // Memanggil fungsi void
    cetakPesan("Hello World!");
    
    // Memanggil langsung dalam cout
    cout << "Luas 2: " << hitungLuas(7, 4) << endl;
    
    return 0;
}
```
### Return
Keyword `return` digunakan di dalam fungsi untuk mengembalikan nilai ke pemanggil fungsi. Saat `return` dijalankan, eksekusi fungsi akan berhenti dan nilai setelah `return` akan dikirimkan kembali ke tempat fungsi tersebut dipanggil.

```cpp linenums="1" title="Contoh pada fungsi hitungLuas"
int hitungLuas(int panjang, int lebar) {
    return panjang * lebar;
}
```
Pada contoh di atas, `return panjang * lebar;` akan mengembalikan hasil perkalian `panjang` dan `lebar` ke pemanggil fungsi. Nilai ini bisa disimpan dalam variabel atau langsung digunakan, seperti pada contoh:

```cpp linenums="1" title="Pemanggilan hitungluas()"
int hasil = hitungLuas(5, 3); // hasil akan bernilai 15
```

### Tipe-tipe Fungsi

Secara umum, fungsi di C++ dapat dikategorikan berdasarkan ada tidaknya parameter dan return value:

| Tipe Fungsi                        | Parameter | Return Value | Contoh Deklarasi                |
|-------------------------------------|-----------|-------------|----------------------------------|
| Fungsi tanpa parameter, tanpa return| Tidak     | Tidak       | `void tampilkanMenu();`          |
| Fungsi tanpa parameter, dengan return| Tidak    | Ya          | `int getNilai();`                |
| Fungsi dengan parameter, tanpa return| Ya       | Tidak       | `void cetakPesan(string pesan);` |
| Fungsi dengan parameter, dengan return| Ya      | Ya          | `int tambah(int a, int b);`      |

#### Contoh Implementasi

```cpp title="Tipe-tipe Fungsi" linenums="1"
// Tanpa parameter, tanpa return
void tampilkanMenu() {
    cout << "1. Tambah\n2. Kurang\n3. Keluar\n";
}

// Tanpa parameter, dengan return
int getNilai() {
    int x;
    cout << "Masukkan nilai: ";
    cin >> x;
    return x;
}

// Dengan parameter, tanpa return
void cetakPesan(string pesan) {
    cout << "Pesan: " << pesan << endl;
}

// Dengan parameter, dengan return
int tambah(int a, int b) {
    return a + b;
}
```

Penggunaan tipe fungsi yang tepat akan membuat kode lebih jelas dan sesuai kebutuhan.

### Parameter dan Argumen

#### Pass by Value
Secara default, C++ menggunakan pass by value, artinya nilai parameter disalin ke dalam fungsi:

```cpp title="Pass by Value" linenums="1"
void tambahSatu(int x) {
    x = x + 1;
    cout << "Dalam fungsi: " << x << endl; // Output: 6
}

int main() {
    int angka = 5;
    tambahSatu(angka);
    cout << "Di main: " << angka << endl; // Output: 5 (tidak berubah)
    return 0;
}
```

#### Pass by Reference
Menggunakan `&` untuk mengubah nilai variabel asli:

```cpp title="Pass by Reference" linenums="1"
void tambahSatu(int &x) {
    x = x + 1;
    cout << "Dalam fungsi: " << x << endl; // Output: 6
}

int main() {
    int angka = 5;
    tambahSatu(angka);
    cout << "Di main: " << angka << endl; // Output: 6 (berubah)
    return 0;
}
```

#### Pass Array ke Fungsi
Array selalu di-pass by reference secara otomatis:

```cpp title="Array sebagai Parameter" linenums="1"
void cetakArray(int arr[], int ukuran) {
    for (int i = 0; i < ukuran; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

void isiArray(int arr[], int ukuran, int nilai) {
    for (int i = 0; i < ukuran; i++) {
        arr[i] = nilai;
    }
}

int main() {
    int data[5] = {1, 2, 3, 4, 5};
    
    cetakArray(data, 5);    // Output: 1 2 3 4 5
    isiArray(data, 5, 0);   // Mengubah semua elemen jadi 0
    cetakArray(data, 5);    // Output: 0 0 0 0 0
    
    return 0;
}
```

### Algoritma dan Utility Functions

#### Contoh Implementasi Algoritma
```cpp title="Binary Search Function" linenums="1"
bool binarySearch(int arr[], int n, int target) {
    int left = 0, right = n - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (arr[mid] == target) {
            return true;
        }
        
        if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return false;
}
```

```cpp title="Bubble Sort Function" linenums="1"
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap elements
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
```

#### Utility Functions
```cpp title="Utility Functions" linenums="1"
// Fungsi untuk menukar dua nilai
void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

// Fungsi untuk cek bilangan prima
bool isPrime(int n) {
    if (n <= 1) return false;
    if (n <= 3) return true;
    if (n % 2 == 0 || n % 3 == 0) return false;
    
    for (int i = 5; i * i <= n; i += 6) {
        if (n % i == 0 || n % (i + 2) == 0) {
            return false;
        }
    }
    return true;
}

// Fungsi untuk menghitung faktorial
long long factorial(int n) {
    if (n <= 1) return 1;
    
    long long result = 1;
    for (int i = 2; i <= n; i++) {
        result *= i;
    }
    return result;
}
```

### Library Functions yang Populer

#### Algorithm Library (`<algorithm>`)
Library ini menyediakan banyak fungsi algoritma yang sangat berguna:

```cpp title="Sort Function" linenums="1"
#include <algorithm>
#include <vector>

int main() {
    // Sort array
    int arr[] = {5, 2, 8, 1, 9, 3};
    int n = 6;
    sort(arr, arr + n);  // Sort ascending
    
    // Sort vector
    vector<int> vec = {5, 2, 8, 1, 9, 3};
    sort(vec.begin(), vec.end());  // Sort ascending
    sort(vec.begin(), vec.end(), greater<int>());  // Sort descending
    
    return 0;
}
```

```cpp title="Max dan Min Functions" linenums="1"
#include <algorithm>

int main() {
    // Max dan Min untuk dua nilai
    int a = 5, b = 3;
    cout << "Max: " << max(a, b) << endl;    // Output: 5
    cout << "Min: " << min(a, b) << endl;    // Output: 3
    
    // Max dan Min dalam array
    int arr[] = {5, 2, 8, 1, 9, 3};
    int n = 6;
    
    int maximum = *max_element(arr, arr + n);  // 9
    int minimum = *min_element(arr, arr + n);  // 1
    
    cout << "Maximum: " << maximum << endl;
    cout << "Minimum: " << minimum << endl;
    
    return 0;
}
```

```cpp title="Binary Search Functions" linenums="1"
#include <algorithm>

int main() {
    int arr[] = {1, 2, 3, 5, 8, 9};  // Harus sudah sorted
    int n = 6;
    
    // Binary search (return true/false)
    bool found = binary_search(arr, arr + n, 5);
    cout << "5 found: " << found << endl;  // Output: 1 (true)
    
    // Lower bound (iterator ke elemen >= target)
    int* pos = lower_bound(arr, arr + n, 5);
    cout << "Lower bound of 5: " << pos - arr << endl;  // Index
    
    // Upper bound (iterator ke elemen > target)
    pos = upper_bound(arr, arr + n, 5);
    cout << "Upper bound of 5: " << pos - arr << endl;  // Index
    
    return 0;
}
```

#### Numeric Library (`<numeric>`)
```cpp title="GCD dan LCM" linenums="1"
#include <numeric>  // C++17 ke atas

int main() {
    int a = 12, b = 18;
    
    // GCD (Greatest Common Divisor)
    int gcd_result = __gcd(a, b);  // GCC specific
    // atau dalam C++17:
    // int gcd_result = gcd(a, b);
    
    // LCM (Least Common Multiple)
    int lcm_result = (a * b) / gcd_result;
    // atau dalam C++17:
    // int lcm_result = lcm(a, b);
    
    cout << "GCD: " << gcd_result << endl;  // Output: 6
    cout << "LCM: " << lcm_result << endl;  // Output: 36
    
    return 0;
}
```

#### Math Library (`<cmath>`)
```cpp title="Math Functions" linenums="1"
#include <cmath>

int main() {
    double x = 16.0;
    
    cout << "sqrt(16): " << sqrt(x) << endl;     // 4
    cout << "pow(2, 3): " << pow(2, 3) << endl;  // 8
    cout << "abs(-5): " << abs(-5) << endl;      // 5
    cout << "ceil(4.3): " << ceil(4.3) << endl;  // 5
    cout << "floor(4.7): " << floor(4.7) << endl; // 4
    
    return 0;
}
```

### Contoh Penggunaan dalam Competitive Programming

```cpp title="Complete Example" linenums="1"
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

// Custom function untuk cek palindrome
bool isPalindrome(string s) {
    int n = s.length();
    for (int i = 0; i < n / 2; i++) {
        if (s[i] != s[n - 1 - i]) {
            return false;
        }
    }
    return true;
}

// Function untuk mencari median
double findMedian(vector<int>& arr) {
    sort(arr.begin(), arr.end());
    int n = arr.size();
    
    if (n % 2 == 1) {
        return arr[n / 2];
    } else {
        return (arr[n / 2 - 1] + arr[n / 2]) / 2.0;
    }
}

int main() {
    // Contoh penggunaan sort
    vector<int> numbers = {5, 2, 8, 1, 9, 3};
    sort(numbers.begin(), numbers.end());
    
    cout << "Sorted: ";
    for (int x : numbers) {
        cout << x << " ";
    }
    cout << endl;
    
    // Contoh penggunaan max/min
    cout << "Max: " << *max_element(numbers.begin(), numbers.end()) << endl;
    cout << "Min: " << *min_element(numbers.begin(), numbers.end()) << endl;
    
    // Contoh penggunaan GCD
    cout << "GCD(12, 18): " << __gcd(12, 18) << endl;
    
    // Contoh penggunaan custom function
    string word = "radar";
    cout << word << " is palindrome: " << isPalindrome(word) << endl;
    
    // Contoh median
    vector<int> data = {1, 3, 2, 5, 4};
    cout << "Median: " << findMedian(data) << endl;
    
    return 0;
}
```

### Tips dan Best Practices

!!! tip "Function Naming"
    Gunakan nama fungsi yang deskriptif dan mengikuti konvensi:
    ```cpp
    // Good
    bool isPrime(int n);
    int calculateSum(int arr[], int size);
    
    // Bad
    bool check(int n);
    int calc(int arr[], int size);
    ```

!!! notes "Parameter Validation"
    Selalu validasi parameter untuk menghindari error:
    ```cpp
    int factorial(int n) {
        if (n < 0) return -1;  // Invalid input
        if (n <= 1) return 1;
        
        // ... rest of the code
    }
    ```

!!! warning "Stack Overflow"
    Hati-hati dengan fungsi yang terlalu dalam atau parameter array yang besar:
    ```cpp
    // Hindari passing array besar by value
    void processArray(int arr[1000000]) {  // Berbahaya!
        // ...
    }
    
    // Lebih baik pass by reference
    void processArray(int arr[], int size) {
        // ...
    }
    ```

### Scope dan Lifetime Variabel

```cpp title="Variable Scope" linenums="1"
int globalVar = 100;  // Global variable

void function1() {
    int localVar = 10;  // Local variable
    cout << globalVar << endl;  // Bisa akses global
    cout << localVar << endl;   // Bisa akses local
}

void function2() {
    cout << globalVar << endl;  // Bisa akses global
    // cout << localVar << endl; // ERROR! localVar tidak bisa diakses
}

int main() {
    function1();
    function2();
    return 0;
}
```


### Kesimpulan
Fungsi adalah konsep fundamental yang memungkinkan kita menulis kode yang modular, dapat digunakan kembali, dan mudah dipelihara. Dengan memahami parameter passing (by value vs by reference), function overloading, dan penggunaan library functions yang populer seperti `sort()`, `max()`, `min()`, `__gcd()`, kita dapat menulis solusi yang lebih efisien dan elegant.

Library functions seperti yang ada di `<algorithm>`, `<numeric>`, dan `<cmath>` sangat membantu dalam competitive programming karena sudah dioptimasi dan terbukti benar. Namun, penting juga untuk bisa mengimplementasi algoritma sendiri untuk memahami cara kerjanya.

### Contoh Soal TLX
- [Memborong Bebek](https://tlx.toki.id/courses/basic-cpp/chapters/07/problems/A)
- [Perkenalan Fungsi](https://tlx.toki.id/courses/basic-cpp/chapters/07/problems/B)
- [Ruang Lingkup Variabel dan Fungsi](https://tlx.toki.id/courses/basic-cpp/chapters/07/problems/D)
- [0 dan > 1 Parameter](https://tlx.toki.id/courses/basic-cpp/chapters/07/problems/E)
- [Fungsi Tanpa Nilai Kembalian](https://tlx.toki.id/courses/basic-cpp/chapters/07/problems/G)
- [Fungsi Anggota](https://tlx.toki.id/courses/basic-cpp/chapters/07/problems/H)
- [Pass by Reference](https://tlx.toki.id/courses/basic-cpp/chapters/07/problems/J)
