# <h1 align="center">Laporan Praktikum Modul 6 - DOUBLY LINKED LIST</h1>
<p align="center">muh rifqi irwanto - 109082500016</p>

## Dasar Teori
A. Doubly Linked List
Daftar terhubung ganda merupakan sebuah struktur data linier di mana setiap node memiliki dua penunjuk, yaitu next yang mengarah ke node selanjutnya dan prev yang mengarah ke node sebelumnya.
Berbeda dengan daftar terhubung tunggal yang hanya memiliki penunjuk untuk node selanjutnya, daftar terhubung ganda memungkinkan untuk navigasi dalam dua arah (maju dan mundur), sehingga proses penambahan dan penghapusan data menjadi lebih mudah.
Setiap node terdiri dari tiga bagian, yaitu informasi (data), penunjuk next, dan penunjuk prev.
Daftar menyimpan dua penunjuk, yaitu First untuk menunjukkan node pertama dan Last untuk menunjukkan node terakhir. Daftar dianggap kosong jika First bernilai Nil (NULL).
Penunjuk prev di node pertama dan penunjuk next di node terakhir juga bernilai Nil sebagai tanda akhir dari daftar.
B. Abstract Data Type (ADT) Bidirectional Linked ListADT merumuskan struktur data bersama dengan operasinya sebagai suatu kesatuan.Dalam tugas ini, ADT dibagi menjadi file header (.h) yang mencakup tipe data dan prototipe fungsi, serta file implementasi (.cpp) yang memuat isi fungsi, lalu diuji pada file main.cpp.Struktur yang dipakai: infotype: informasi yang disimpan (contoh kode buku, judul, tahun terbit) ElmList: node (memuat info, next, dan prev) address: penunjuk ke ElmList List: struktur yang terdiri dari First dan LastC. Operasi Fundamental dan Penambahan InformasiOperasi fundamental mencakup CreateList untuk menghasilkan daftar kosong (First dan Last diisi dengan Nil), alokasi untuk menciptakan node baru secara dinamis menggunakan operator new, dealokasi untuk membebaskan ruang memori dengan operator delete, dan printInfo untuk menampilkan informasi dengan menjelajahi daftar. Fungsi insertLast menambahkan simpul di akhir daftar: jika daftar kosong, simpul baru menjadi First dan Last, jika tidak, simpul sebelumnya diarahkan ke Last lama, simpul next Last lama diarahkan ke simpul baru, kemudian Last diperbarui. Penyisipan dalam doubly linked list dapat dilakukan di awal, di akhir, atau di tengah list [5].D. Pencarian pada Daftar Terhubung GandaPencarian dilakukan dengan menjelajahi node dari First menggunakan pointer next sambil membandingkan data yang dicari (dalam tugas ini kodeBuku atau nopol) dengan informasi di setiap node. Fungsi findElm memberikan alamat node yang sesuai, atau Nil jika tidak ada. Metode ini dikenal sebagai pencarian linear dengan kompleksitas waktu O(n), karena dalam kasus paling buruk, setiap node harus diperiksa. Dalam tugas ini, pencarian juga digunakan untuk memeriksa duplikasi sebelum data yang baru ditambahkan.
C. Operasi Fundamental dan Penambahan InformasiOperasi fundamental mencakup CreateList untuk menghasilkan daftar kosong (First dan Last diisi dengan Nil), alokasi untuk menciptakan node baru secara dinamis menggunakan operator new, dealokasi untuk membebaskan ruang memori dengan operator delete, dan printInfo untuk menampilkan informasi dengan menjelajahi daftar. Fungsi insertLast menambahkan simpul di akhir daftar: jika daftar kosong, simpul baru menjadi First dan Last, jika tidak, simpul sebelumnya diarahkan ke Last lama, simpul next Last lama diarahkan ke simpul baru, kemudian Last diperbarui. Penyisipan dalam doubly linked list dapat dilakukan di awal, di akhir, atau di tengah list [5].
D. Pencarian pada Daftar Terhubung GandaPencarian dilakukan dengan menjelajahi node dari First menggunakan pointer next sambil membandingkan data yang dicari (dalam tugas ini kodeBuku atau nopol) dengan informasi di setiap node. Fungsi findElm memberikan alamat node yang sesuai, atau Nil jika tidak ada. Metode ini dikenal sebagai pencarian linear dengan kompleksitas waktu O(n), karena dalam kasus paling buruk, setiap node harus diperiksa. Dalam tugas ini, pencarian juga digunakan untuk memeriksa duplikasi sebelum data yang baru ditambahkan.
E. Penghilangan Data (Hapus)Penghapusan dalam doubly linked list dapat dilakukan di bagian awal, akhir, atau tengah list [5]. deleteFirst menghapus node pertama dan memindahkan First, deleteLast menghapus node terakhir dan memindahkan Last, sedangkan deleteAfter menghapus node yang tepat setelah node Prec dengan menghubungkan kembali pointer next dan prev.

## Guided 

### 1.Program Doublylinkedlist
```C++
// File: doublylist.h
#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H

#include <iostream>
#include <string>

#define Nil NULL

// Latihan 1
struct infotype {
    std::string nopol; 
    std::string warna; 
    int thnBuat;      
};
typedef struct elmlist *address;
struct elmlist {
    infotype info;  
    address next;   
    address prev;   
};
struct List {
    address First; 
    address Last;  
};


// Latihan 1
void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertLast(List &L, address P);

// Latihan 2

address findElm(List L, std::string nopol);

// Latihan 3
void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(List &L, address Prec, address &P);
void deleteElm(List &L, std::string nopol, bool &status);

#endif
// File: doublylist.cpp
#include "doublylist.h"

// Latihan 1
void CreateList(List &L) {
    L.First = Nil;
    L.Last = Nil;
}

address alokasi(infotype x) {
    address P = new elmlist;
    P->info = x;
    P->next = Nil;
    P->prev = Nil; 
    return P;
}

void dealokasi(address &P) {
    delete P;
}

void printInfo(List L) {
    address P = L.Last;
    if (P == Nil) {
        std::cout << "List kosong." << std::endl;
        return;
    }
    while (P != Nil) {
        std::cout << "no polisi : " << P->info.nopol << std::endl;   
        std::cout << "warna     : " << P->info.warna << std::endl;   
        std::cout << "tahun     : " << P->info.thnBuat << std::endl; 
        P = P->prev;
    }
}

void insertLast(List &L, address P) {
    if (L.First == Nil) { 
        L.First = P;
        L.Last = P;
    } else {
        P->prev = L.Last;         
        (L.Last)->next = P;     
        L.Last = P;               
    }
}

// Latihan 2
address findElm(List L, std::string nopol) {
    address P = L.First;
    while (P != Nil) {
        if (P->info.nopol == nopol) {
            return P;
        }
        P = P->next;
    }
    return Nil;
}

// Latihan 3
void deleteFirst(List &L, address &P) {
    if (L.First == Nil) return;

    P = L.First; 
    if (L.First == L.Last) { 
        L.First = Nil;
        L.Last = Nil;
    } else {
        L.First = P->next;     
        (L.First)->prev = Nil; 
        P->next = Nil;         
    }
}

void deleteLast(List &L, address &P) {
    if (L.First == Nil) return;

    P = L.Last; 
    if (L.First == L.Last) { 
        L.First = Nil;
        L.Last = Nil;
    } else {
        L.Last = P->prev;      
        (L.Last)->next = Nil; 
        P->prev = Nil;         
    }
}

void deleteAfter(List &L, address Prec, address &P) {
    if (Prec == Nil || Prec->next == Nil) return;

    P = Prec->next;
    if (P == L.Last) {
        deleteLast(L, P);
    } else {
        Prec->next = P->next;     
        (P->next)->prev = Prec; 
        P->next = Nil;            
        P->prev = Nil;           
    }
}

void deleteElm(List &L, std::string nopol, bool &status) {
    address P = findElm(L, nopol);
    status = false;

    if (P != Nil) {
        if (P == L.First) {
            deleteFirst(L, P);
        } else if (P == L.Last) {
            deleteLast(L, P);
        } else {
            address Prec = P->prev;
            deleteAfter(L, Prec, P);
        }
        dealokasi(P); 
        status = true;
    }
}
// File: main.cpp
#include <iostream>
#include "Doublylist.h"
using namespace std;

void inputData(List &L) {
    infotype data;
    address P;

    cout << "masukkan nomor polisi: "; cin >> data.nopol;
    cout << "masukkan warna kendaraan: "; cin >> data.warna;
    cout << "masukkan tahun kendaraan: "; cin >> data.thnBuat;
    if (findElm(L, data.nopol) == Nil) {
        P = alokasi(data); 
        insertLast(L, P);  
    } else {
        cout << "nomor polisi sudah terdaftar" << endl; 
    }
}

int main() {
    List L;
    CreateList(L); 
    address P;

    // Latihan 1
    inputData(L); 
    inputData(L); 
    inputData(L); 
    inputData(L); 

    cout << "\nDATA LIST 1" << endl; 
    printInfo(L); 

    // Latihan 2
    string nopolCari;
    cout << "\nMasukkan Nomor Polisi yang dicari : "; 
    cin >> nopolCari; 
    
    P = findElm(L, nopolCari); 
    if (P != Nil) {
        cout << "Nomor Polisi : " << P->info.nopol << endl; 
        cout << "Warna        : " << P->info.warna << endl; 
        cout << "Tahun        : " << P->info.thnBuat << endl; 
    } else {
        cout << "Data dengan nomor polisi " << nopolCari << " tidak ditemukan." << endl;
    }

    // Latihan 3
    string nopolHapus;
    bool hapusBerhasil;
    cout << "\nMasukkan Nomor Polisi yang akan dihapus : ";
    cin >> nopolHapus;

    deleteElm(L, nopolHapus, hapusBerhasil); 

    if (hapusBerhasil) {
        cout << "Data dengan nomor polisi " << nopolHapus << " berhasil dihapus." << endl; 
    } else {
        cout << "Data dengan nomor polisi " << nopolHapus << " tidak ditemukan." << endl;
    }
    cout << "\nDATA LIST 1" << endl; 
    printInfo(L); 

    return 0;
}

```
Program ini menyimpan informasi buku (kode, judul, tahun terbit) dalam linked list ganda. buku.h mencakup struktur data dan daftar fungsi, buku.cpp mengimplementasikan fungsi-fungsinya (membuat list, alokasi, mencetak, menambah di akhir, mencari, dan tiga jenis penghapusan), sedangkan bukumain.cpp menjalankan alurnya: memasukkan data dengan pemeriksaan kode ganda, mencari satu buku, dan menghapus satu buku.

## Unguided 

### 1. Program ADT Doubly Linked List - Insert First
```C++

File: Book.h
#ifndef BUKU_H_INCLUDED
#define BUKU_H_INCLUDED

#include <iostream>
#include <string>
using namespace std;

struct buku {
    string kodeBuku;
    string judul;
    int thnTerbit;
};
typedef buku infotype;

typedef struct ElmList *address;
struct ElmList {
    infotype info;
    address next;
    address prev;
};

struct List {
    address First;
    address Last;
};

void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertLast(List &L, address P);

#endif 
File: Book.cpp
#include "Book.h"

void CreateList(List &L) {
    L.First = NULL;
    L.Last = NULL;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = NULL;
    P->prev = NULL;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = NULL;
}

void printInfo(List L) {
    address P = L.Last;
    while (P != NULL) {
        cout << "kode buku : " << P->info.kodeBuku << endl;
        cout << "judul     : " << P->info.judul << endl;
        cout << "tahun     : " << P->info.thnTerbit << endl;
        P = P->prev;
    }
}

void insertLast(List &L, address P) {
    if (L.First == NULL) {
        L.First = P;
        L.Last = P;
    } else {
        P->prev = L.Last;
        L.Last->next = P;
        L.Last = P;
    }
}

File: main.cpp
#include "Book.h"

bool sudahTerdaftar(List L, string kode) {
    address P = L.First;
    while (P != NULL) {
        if (P->info.kodeBuku == kode) {
            return true;
        }
        P = P->next;
    }
    return false;
}

int main() {
    List L;
    CreateList(L);
    infotype x;

    for (int i = 0; i < 4; i++) {
        cout << "masukkan kode buku: ";
        cin >> x.kodeBuku;
        cout << "masukkan judul buku: ";
        cin >> x.judul;
        cout << "masukkan tahun terbit: ";
        cin >> x.thnTerbit;

        if (sudahTerdaftar(L, x.kodeBuku)) {
            cout << "kode buku sudah terdaftar" << endl;
        } else {
            insertLast(L, alokasi(x));
        }
        cout << endl;
    }

    cout << "DATA LIST 1" << endl;
    printInfo(L);

    return 0;
}
```
Program ini dimulai dengan membuat list kosong melalui prosedur CreateList, lalu pengguna memasukkan empat data buku yang meliputi kode buku, judul, dan tahun penerbitan. Setiap kode buku diperiksa dengan fungsi sudahTerdaftar untuk memastikan tidak ada kode yang duplikat. Apabila kode belum terdaftar, data buku akan dijadikan node baru melalui fungsi alokasi dan ditambahkan ke akhir list menggunakan prosedur insertLast. Setelah semua informasi dimasukkan, fungsi printInfo menampilkan seluruh data buku dengan mengeksplorasi daftar dari Last ke First menggunakan pointer prev, sehingga data ditampilkan dalam urutan terbalik dari urutan penyimpanan. Oleh karena itu, program ini menggunakan struktur data Double Linked List untuk menyimpan dan menampilkan informasi buku serta menghindari adanya kode buku yang sama.### Output Unguided 1 :

### 2.Pencarian 
```C++
File: Book.h

#ifndef BUKU_H_INCLUDED
#define BUKU_H_INCLUDED

#include <iostream>
#include <string>
using namespace std;

struct buku {
    string kodeBuku;
    string judul;
    int thnTerbit;
};
typedef buku infotype;

typedef struct ElmList *address;
struct ElmList {
    infotype info;
    address next;
    address prev;
};

struct List {
    address First;
    address Last;
};

void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertLast(List &L, address P);

address findElm(List L, infotype x);

#endif 
File: Book.cpp

#include "Book.h"

void CreateList(List &L) {
    L.First = NULL;
    L.Last = NULL;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = NULL;
    P->prev = NULL;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = NULL;
}

void printInfo(List L) {
    address P = L.Last;
    while (P != NULL) {
        cout << "kode buku : " << P->info.kodeBuku << endl;
        cout << "judul     : " << P->info.judul << endl;
        cout << "tahun     : " << P->info.thnTerbit << endl;
        P = P->prev;
    }
}

void insertLast(List &L, address P) {
    if (L.First == NULL) {
        L.First = P;
        L.Last = P;
    } else {
        P->prev = L.Last;
        L.Last->next = P;
        L.Last = P;
    }
}

address findElm(List L, infotype x) {
    address P = L.First;
    while (P != NULL) {
        if (P->info.kodeBuku == x.kodeBuku) {
            return P;
        }
        P = P->next;
    }
    return NULL;
}
File: main.cpp
#include "Book.h"

void tambahData(List &L, string kode, string judul, int thn) {
    infotype x;
    x.kodeBuku = kode;
    x.judul = judul;
    x.thnTerbit = thn;
    insertLast(L, alokasi(x));
}

int main() {
    List L;
    CreateList(L);

    tambahData(L, "B001", "Algoritma", 2020);
    tambahData(L, "B003", "Struktur_Data", 2018);
    tambahData(L, "B004", "Jaringan_Komputer", 2022);

    infotype x;
    cout << "Masukkan Kode Buku yang dicari : ";
    cin >> x.kodeBuku;
    cout << endl;

    address P = findElm(L, x);
    if (P != NULL) {
        cout << "Kode Buku    : " << P->info.kodeBuku << endl;
        cout << "Judul        : " << P->info.judul << endl;
        cout << "Tahun Terbit : " << P->info.thnTerbit << endl;
    } else {
        cout << "Data tidak ditemukan." << endl;
    }

    return 0;
}
```
Program ini dimulai dengan membuat list kosong menggunakan prosedur CreateList, lalu memasukkan tiga data buku melalui fungsi tambahData, yaitu buku dengan kode B001, B003, dan B004. Setiap informasi buku disimpan sebagai node baru dan dimasukkan ke akhir daftar menggunakan prosedur insertLast. Setelah itu, pengguna diminta untuk memasukkan kode buku yang ingin dicari. Fungsi findElm akan menjelajahi daftar dari First dengan menggunakan pointer next untuk mencocokkan kode buku yang diberikan dengan kode yang tersimpan. Apabila kode buku berhasil ditemukan, program akan menampilkan kode, judul, dan tahun terbit dari buku tersebut. Sebaliknya, apabila kode tidak ditemukan, program akan menampilkan pesan “Data tidak tersedia.” Program ini menggunakan struktur data Double Linked List untuk menyimpan informasi buku dan melakukan pencarian berdasarkan kode buku.
### 3. Mengdelete
```C++
File: Book.h

#ifndef BUKU_H_INCLUDED
#define BUKU_H_INCLUDED

#include <iostream>
#include <string>
using namespace std;

struct buku {
    string kodeBuku;
    string judul;
    int thnTerbit;
};
typedef buku infotype;

typedef struct ElmList *address;
struct ElmList {
    infotype info;
    address next;
    address prev;
};

struct List {
    address First;
    address Last;
};

void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertLast(List &L, address P);

address findElm(List L, infotype x);

void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(address Prec, address &P);

#endif 
File: Book.cpp

#include "Book.h"

void CreateList(List &L) {
    L.First = NULL;
    L.Last = NULL;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = NULL;
    P->prev = NULL;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = NULL;
}

void printInfo(List L) {
    address P = L.Last;
    while (P != NULL) {
        cout << "Kode Buku    : " << P->info.kodeBuku << endl;
        cout << "Judul        : " << P->info.judul << endl;
        cout << "Tahun Terbit : " << P->info.thnTerbit << endl;
        P = P->prev;
    }
}

void insertLast(List &L, address P) {
    if (L.First == NULL) {
        L.First = P;
        L.Last = P;
    } else {
        P->prev = L.Last;
        L.Last->next = P;
        L.Last = P;
    }
}

address findElm(List L, infotype x) {
    address P = L.First;
    while (P != NULL) {
        if (P->info.kodeBuku == x.kodeBuku) {
            return P;
        }
        P = P->next;
    }
    return NULL;
}

void deleteFirst(List &L, address &P) {
    if (L.First == NULL) {
        P = NULL;
    } else if (L.First == L.Last) {
        P = L.First;
        L.First = NULL;
        L.Last = NULL;
    } else {
        P = L.First;
        L.First = P->next;
        L.First->prev = NULL;
        P->next = NULL;
    }
}

void deleteLast(List &L, address &P) {
    if (L.First == NULL) {
        P = NULL;
    } else if (L.First == L.Last) {
        P = L.Last;
        L.First = NULL;
        L.Last = NULL;
    } else {
        P = L.Last;
        L.Last = P->prev;
        L.Last->next = NULL;
        P->prev = NULL;
    }
}

void deleteAfter(address Prec, address &P) {
    if (Prec == NULL || Prec->next == NULL) {
        P = NULL;
    } else {
        P = Prec->next;
        Prec->next = P->next;
        if (P->next != NULL) {
            P->next->prev = Prec;
        }
        P->next = NULL;
        P->prev = NULL;
    }
}
File: main.cpp
#include "Book.h"

void tambahData(List &L, string kode, string judul, int thn) {
    infotype x;
    x.kodeBuku = kode;
    x.judul = judul;
    x.thnTerbit = thn;
    insertLast(L, alokasi(x));
}

int main() {
    List L;
    CreateList(L);

    tambahData(L, "B001", "Algoritma", 2020);
    tambahData(L, "B003", "Struktur_Data", 2018);
    tambahData(L, "B004", "Jaringan_Komputer", 2022);

    infotype x;
    cout << "Masukkan Kode Buku yang akan dihapus : ";
    cin >> x.kodeBuku;

    address P = findElm(L, x);
    if (P == NULL) {
        cout << "Data tidak ditemukan." << endl;
    } else {
        address Q;
        if (P == L.First) {
            deleteFirst(L, Q);
        } else if (P == L.Last) {
            deleteLast(L, Q);
        } else {
            deleteAfter(P->prev, Q);
        }
        dealokasi(Q);
        cout << "Data dengan kode buku " << x.kodeBuku << " berhasil dihapus." << endl;
    }

    cout << endl << "DATA LIST 1" << endl;
    printInfo(L);

    return 0;
}
```
Program ini dimulai dengan membuat daftar kosong melalui prosedur CreateList, lalu menambahkan tiga data buku dengan menggunakan fungsi tambahData. Setelah itu, pengguna diminta untuk menginput kode buku yang ingin dihapus. Fungsi findElm berfungsi untuk menemukan buku dengan berdasarkan kode yang sudah dimasukkan. Apabila data ditemukan, program akan menghapusnya dengan prosedur deleteFirst jika terletak di awal list, deleteLast jika berada di akhir list, atau deleteAfter jika posisinya di tengah list. Selanjutnya, fungsi dealokasi digunakan untuk mengosongkan memori node yang telah dihapus. Jika data tidak ada, program akan menunjukkan pesan bahwa data tidak ada. Akhirnya, fungsi printInfo akan menunjukkan data buku yang tersisa dalam daftar dari akhir ke awal. Oleh karena itu, program ini menggunakan Double Linked List untuk menyimpan, mencari, dan menghapus informasi buku berdasarkan kode buku.

## Kesimpulan
Kesimpulan dari semua program di atas adalah bahwa struktur data Double Linked List dapat dimanfaatkan untuk mengelola informasi buku, mulai dari menambah data, mencari buku berdasarkan kode, sampai menghapus data buku yang diinginkan.

