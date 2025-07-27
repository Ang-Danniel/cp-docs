# String
String merupakan struktur data fundamental yang sangat penting dalam pemrograman dan akan **selalu muncul** di berbagai soal kompetitif, mulai dari manipulasi teks, parsing input, pattern matching, hingga algoritma string. Dengan memahami string dan method-methodnya, kita dapat mengolah data teks dengan efisien dan menyelesaikan berbagai permasalahan yang melibatkan karakter dan kata.

### Pengenalan
Mari kita mulai dengan contoh permasalahan sederhana:

> Simpan nama lengkap seseorang dan tampilkan informasi tentangnya.

Jika kita menulis:
```cpp linenums="1"
char huruf1 = 'J';
char huruf2 = 'o';
char huruf3 = 'h';
char huruf4 = 'n';
// ... dan seterusnya
```
Maka jelas, ini tidak efisien. Di sinilah string dibutuhkan: kita bisa menyimpan rangkaian karakter dalam satu variabel dan memanipulasinya dengan mudah.

### Deklarasi String
String dalam C++ dapat direpresentasikan dalam dua cara utama: sebagai array karakter (C-style) atau sebagai objek string (C++ style).

```cpp title="Deklarasi String" linenums="1"
// C-style string (array karakter)
char nama[50];

// C++ style string (objek string)
string nama;
```

```cpp title="Contoh Deklarasi dan Inisialisasi" linenums="1"
#include <iostream>
#include <string>
using namespace std;

int main() {
    // Berbagai cara deklarasi string
    string greeting = "Hello";          // Inisialisasi langsung
    string name("World");               // Constructor
    string message;                     // String kosong
    char cstr[] = "Hello World";        // C-style string
    
    return 0;
}
```

Kegunaan umum di pemrograman kompetitif:

- Parsing dan manipulasi input teks
- Pattern matching dan string searching
- Implementasi algoritma string (KMP, Z-algorithm)
- Validasi format data

### Input dan Output String

#### Input String
```cpp title="Input String Sederhana" linenums="1"
string kata;
cin >> kata;  // Membaca satu kata (sampai spasi)
cout << "Kata: " << kata << endl;
```

```cpp title="Input String dengan Spasi" linenums="1"
string kalimat;
getline(cin, kalimat);  // Membaca satu baris lengkap
cout << "Kalimat: " << kalimat << endl;
```

```cpp title="Kombinasi Input" linenums="1"
int n;
string nama;

cin >> n;              // Baca integer
cin.ignore();          // Bersihkan newline dari buffer
getline(cin, nama);    // Baca string dengan spasi
```

#### Output String
```cpp title="Output String" linenums="1"
string message = "Hello World";
cout << message << endl;
cout << "Panjang: " << message.length() << endl;
```

### Method-Method String yang Penting

#### Length dan Size
```cpp title="Mengukur Panjang String" linenums="1"
string text = "Programming";
cout << "Length: " << text.length() << endl;  // Output: 11
cout << "Size: " << text.size() << endl;      // Output: 11 (sama dengan length)
cout << "Empty: " << text.empty() << endl;    // Output: 0 (false)

string kosong = "";
cout << "Empty: " << kosong.empty() << endl;  // Output: 1 (true)
```

#### Akses Karakter
```cpp title="Mengakses Karakter Individual" linenums="1"
string word = "Hello";

// Menggunakan operator []
cout << "Karakter pertama: " << word[0] << endl;    // H
cout << "Karakter terakhir: " << word[4] << endl;   // o

// Menggunakan method at()
cout << "Karakter kedua: " << word.at(1) << endl;   // e

// Method front() dan back()
cout << "Depan: " << word.front() << endl;          // H
cout << "Belakang: " << word.back() << endl;        // o
```

#### Concatenation (Penggabungan)
```cpp title="Menggabungkan String" linenums="1"
string first = "Hello";
string second = "World";

// Menggunakan operator +
string result1 = first + " " + second;
cout << result1 << endl;  // Hello World

// Menggunakan operator +=
first += " ";
first += second;
cout << first << endl;    // Hello World

// Menggunakan append()
string greeting = "Hi";
greeting.append(" there");
cout << greeting << endl; // Hi there
```

#### Substring
```cpp title="Mengambil Bagian String" linenums="1"
string text = "Programming";

// substr(start_pos, length)
string sub1 = text.substr(0, 4);    // "Prog"
string sub2 = text.substr(4);       // "ramming" (dari indeks 4 sampai akhir)
string sub3 = text.substr(4, 3);    // "ram"

cout << sub1 << endl;
cout << sub2 << endl;
cout << sub3 << endl;
```

#### Find dan Search
```cpp title="Mencari dalam String" linenums="1"
string sentence = "I love programming and programming loves me";

// Mencari substring
size_t pos = sentence.find("programming");
if (pos != string::npos) {
    cout << "Found at position: " << pos << endl;  // Output: 7
}

// Mencari dari posisi tertentu
size_t pos2 = sentence.find("programming", pos + 1);
if (pos2 != string::npos) {
    cout << "Found again at: " << pos2 << endl;   // Output: 24
}

// Mencari karakter
size_t char_pos = sentence.find('o');
cout << "First 'o' at: " << char_pos << endl;    // Output: 5

// rfind - mencari dari belakang
size_t last_pos = sentence.rfind("programming");
cout << "Last occurrence: " << last_pos << endl;  // Output: 24
```

#### Replace
```cpp title="Mengganti Bagian String" linenums="1"
string text = "I like apples and apples are good";

// replace(start_pos, length, new_string)
text.replace(7, 6, "oranges");  // Ganti "apples" dengan "oranges"
cout << text << endl;  // I like oranges and apples are good

// Mengganti semua kemunculan
string original = "cat cat cat";
string target = "cat";
string replacement = "dog";

size_t pos = 0;
while ((pos = original.find(target, pos)) != string::npos) {
    original.replace(pos, target.length(), replacement);
    pos += replacement.length();
}
cout << original << endl;  // dog dog dog
```

#### Insert dan Erase
```cpp title="Menyisipkan dan Menghapus" linenums="1"
string text = "Hello World";

// Insert - menyisipkan string
text.insert(5, " Beautiful");
cout << text << endl;  // Hello Beautiful World

// Erase - menghapus bagian string
text.erase(5, 10);     // Hapus " Beautiful"
cout << text << endl;  // Hello World

// Erase dari posisi tertentu sampai akhir
string sample = "Programming";
sample.erase(4);       // Hapus dari indeks 4 sampai akhir
cout << sample << endl; // Prog
```

#### Compare
```cpp title="Membandingkan String" linenums="1"
string str1 = "Apple";
string str2 = "Banana";
string str3 = "Apple";

// Menggunakan operator ==, !=, <, >, <=, >=
cout << (str1 == str3) << endl;  // 1 (true)
cout << (str1 < str2) << endl;   // 1 (true, karena A < B)

// Menggunakan method compare()
int result = str1.compare(str2);
if (result < 0) {
    cout << str1 << " < " << str2 << endl;
} else if (result > 0) {
    cout << str1 << " > " << str2 << endl;
} else {
    cout << str1 << " == " << str2 << endl;
}
```

### Konversi String

#### String ke Angka
```cpp title="String to Number" linenums="1"
#include <string>

string num_str = "123";
string float_str = "45.67";

// C++11 methods
int num = stoi(num_str);           // string to int
long long_num = stol(num_str);     // string to long
float f = stof(float_str);         // string to float
double d = stod(float_str);        // string to double

cout << "Integer: " << num << endl;
cout << "Double: " << d << endl;
```

#### Angka ke String
```cpp title="Number to String" linenums="1"
int number = 42;
double pi = 3.14159;

// C++11 method
string str_num = to_string(number);
string str_pi = to_string(pi);

cout << "String number: " << str_num << endl;
cout << "String pi: " << str_pi << endl;
```

### Iterasi String
String dapat diiterasi seperti array:

```cpp title="Iterasi String" linenums="1"
string word = "Hello";

// Menggunakan index
for (int i = 0; i < word.length(); i++) {
    cout << word[i] << " ";
}
cout << endl;

// Menggunakan range-based for loop (C++11)
for (char c : word) {
    cout << c << " ";
}
cout << endl;

// Menggunakan iterator
for (auto it = word.begin(); it != word.end(); it++) {
    cout << *it << " ";
}
cout << endl;
```

### Contoh Aplikasi Praktis

#### Validasi Input
```cpp title="Validasi Email Sederhana" linenums="1"
bool isValidEmail(string email) {
    size_t at_pos = email.find('@');
    size_t dot_pos = email.rfind('.');
    
    return (at_pos != string::npos && 
            dot_pos != string::npos && 
            at_pos < dot_pos &&
            at_pos > 0 &&
            dot_pos < email.length() - 1);
}

int main() {
    string email;
    cout << "Masukkan email: ";
    cin >> email;
    
    if (isValidEmail(email)) {
        cout << "Email valid" << endl;
    } else {
        cout << "Email tidak valid" << endl;
    }
    
    return 0;
}
```

#### Word Count
```cpp title="Menghitung Kata" linenums="1"
int countWords(string sentence) {
    if (sentence.empty()) return 0;
    
    int count = 0;
    bool inWord = false;
    
    for (char c : sentence) {
        if (c != ' ' && !inWord) {
            inWord = true;
            count++;
        } else if (c == ' ') {
            inWord = false;
        }
    }
    
    return count;
}

int main() {
    string text = "Hello world programming";
    cout << "Jumlah kata: " << countWords(text) << endl;  // Output: 3
    return 0;
}
```

#### Palindrome Check
```cpp title="Cek Palindrome" linenums="1"
bool isPalindrome(string str) {
    // Convert to lowercase dan hapus spasi
    string clean = "";
    for (char c : str) {
        if (c != ' ') {
            clean += tolower(c);
        }
    }
    
    int left = 0;
    int right = clean.length() - 1;
    
    while (left < right) {
        if (clean[left] != clean[right]) {
            return false;
        }
        left++;
        right--;
    }
    
    return true;
}

int main() {
    string word = "A man a plan a canal Panama";
    cout << word << " is palindrome: " << isPalindrome(word) << endl;
    return 0;
}
```

#### String Tokenization
```cpp title="Memisahkan String" linenums="1"
vector<string> split(string str, char delimiter) {
    vector<string> tokens;
    string token = "";
    
    for (char c : str) {
        if (c == delimiter) {
            if (!token.empty()) {
                tokens.push_back(token);
                token = "";
            }
        } else {
            token += c;
        }
    }
    
    if (!token.empty()) {
        tokens.push_back(token);
    }
    
    return tokens;
}

int main() {
    string data = "apple,banana,orange,grape";
    vector<string> fruits = split(data, ',');
    
    for (string fruit : fruits) {
        cout << fruit << endl;
    }
    
    return 0;
}
```

### Tips dan Best Practices

!!! tip "String Efficiency"
    Untuk operasi string yang banyak, pertimbangkan menggunakan `reserve()` untuk menghindari realokasi:
    ```cpp
    string result;
    result.reserve(1000);  // Reserve space untuk 1000 karakter
    
    for (int i = 0; i < 100; i++) {
        result += "test";
    }
    ```

!!! notes "String Comparison"
    Perbandingan string bersifat lexicographical (berdasarkan ASCII):
    ```cpp
    string a = "Apple";
    string b = "Banana";
    cout << (a < b) << endl;  // true, karena 'A' < 'B'
    
    // Untuk case-insensitive comparison:
    transform(a.begin(), a.end(), a.begin(), ::tolower);
    transform(b.begin(), b.end(), b.begin(), ::tolower);
    ```

!!! warning "Index Out of Bounds"
    Selalu periksa bounds saat mengakses karakter:
    ```cpp
    string text = "Hello";
    if (index < text.length()) {
        char c = text[index];  // Safe access
    }
    
    // Atau gunakan at() yang throw exception
    try {
        char c = text.at(index);
    } catch (out_of_range& e) {
        cout << "Index out of bounds!" << endl;
    }
    ```

### Algorithm Library untuk String

```cpp title="Useful String Algorithms" linenums="1"
#include <algorithm>
#include <string>

int main() {
    string text = "Programming";
    
    // Reverse string
    reverse(text.begin(), text.end());
    cout << text << endl;  // gnimmargorP
    
    // Sort karakter dalam string
    string word = "hello";
    sort(word.begin(), word.end());
    cout << word << endl;  // ehllo
    
    // Remove duplicates
    string dup = "programming";
    sort(dup.begin(), dup.end());
    dup.erase(unique(dup.begin(), dup.end()), dup.end());
    cout << dup << endl;  // agimnopr
    
    // Transform to uppercase
    string lower = "hello world";
    transform(lower.begin(), lower.end(), lower.begin(), ::toupper);
    cout << lower << endl;  // HELLO WORLD
    
    return 0;
}
```

### Kesimpulan
String adalah struktur data fundamental yang memungkinkan kita menyimpan dan memanipulasi data teks dengan efisien. Dengan memahami berbagai method seperti `find()`, `substr()`, `replace()`, `insert()`, dan `erase()`, kita dapat menyelesaikan berbagai permasalahan yang melibatkan pemrosesan teks.
