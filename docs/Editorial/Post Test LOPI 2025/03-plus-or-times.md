# Plus or Times

**Link Soal:** [INC 2022 - Problem G](link-soal-disini)  
**Sumber:** INC 2022 / TLX
**Tingkat Kesulitan:** Medium 
**Tag:** DP

## Overview Permasalahan

Terdapat sebuah permainan dimana anda ingin initial point anda yaitu p menjadi semaksium mungkin dengan mengikuti beberapa ronde permaianan.

Disetiap rondenya anda ingin mengubah point p yang anda miiliki sekarang dengan melakukan salah satu operasi yang ada.

Tiap ronde akan terdapat 2 operasi yang dimana operasi tersebut bisa tambah atau pekalian dengan suatu bilangan. 

Anda wajib memilih satu operasi yang ada ke poin yang anda miliki. Tentukan p maksimum yang bisa anda raih.

## Hints

??? info "Hint 1"
    
    Anda bisa melakukan DP disini :3.

## Solusi

??? success "Solusi"
    
    Anggap maxx[i] sebagai nilai paling maksimum P jika terdapat i ronde saja dan minn[i] sebagai nilai paling minimum P jika terdapat i ronde saja. 
    
    Maka perhatikan bahwa maxx[i] bisa didapatkan dengan maxx[i-1] dan minn[i-1] saja. Hal ini benar karena dengan nilai paling minimum p dapat menjadi nilai paling maksimum jika minn[i-1] negatif dan terdapat operasi kali negatif yang dapat membuat menjadi nilai negatif yang besar.

    Sehingga
    `maxx[i] = max(minn[i-1] op1 c1, maxx[i-1] op1 c1);`
    `maxx[i] = max(maxx[i], maxx[i-1] op2 c2);`
    `maxx[i] = max(maxx[i], minn[i-1] op2 c2);`

    `minn[i] = min(minn[i-1] op1 c1, maxx[i-1] op1 c1);`
    `minn[i] = min(minn[i], maxx[i-1] op2 c2);`
    `minn[i] = min(minn[i], minn[i-1] op2 c2);`

    - **Time Complexity:** O(N)
    - **Space Complexity:** O(1)

### Implementasi

??? example "Implementasi"

    ```cpp title="Solution" linenums="1"
    ll n, p; cin >> n >> p;
    ll maxx, minn;
    maxx = minn = p;
    for (int i = 0; i < n; i++) {
        char op; cin >> op;
        ll input; cin >> input;
        ll tempMax1, tempMin1;
        if (op == '+') {
            tempMax1 = maxx + input;
            tempMin1 = minn + input;
        } else {
            tempMax1 = maxx * input;
            tempMin1 = minn * input;
        }
        
        cin >> op;
        cin >> input;
        ll tempMax2, tempMin2;
        if (op == '+') {
            tempMax2 = maxx + input;
            tempMin2 = minn + input;
        } else {
            tempMax2 = maxx * input;
            tempMin2 = minn * input;
        }

        maxx = max(tempMax1, tempMax2);
        maxx = max(maxx, tempMin2);
        maxx = max(tempMin1, maxx);

        minn = min(tempMax1, tempMax2);
        minn = min(tempMin1, minn);
        minn = min(minn, tempMin2);
    }
    cout << maxx << endl;
    ```

:3
