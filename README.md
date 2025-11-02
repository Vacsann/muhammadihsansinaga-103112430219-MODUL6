# muhammadihsansinaga-103112430219-MODUL6
LAPRAK MODUL 6
# <h1 align="center">Laporan Praktikum Modul 6 <br> Doubly Linked List (BAGIAN PERTAMA) </h1>
<p align="center">MUHAMMAD IHSAN SINAGA - 103112430219</p>

## Dasar Teori

Doubly Linked List adalah struktur data dinamis yang terdiri dari rangkaian node, di mana setiap node memiliki tiga bagian: data, pointer ke node berikutnya (next), dan pointer ke node sebelumnya (prev). Berbeda dengan singly linked list yang hanya dapat ditelusuri satu arah, struktur ini memungkinkan pergerakan maju maupun mundur karena adanya dua pointer penghubung. Node pertama biasanya ditandai dengan pointer first, sedangkan node terakhir ditandai dengan last. Keunggulan Doubly Linked List terletak pada kemudahan dalam melakukan operasi penyisipan dan penghapusan dari kedua ujung list, namun kekurangannya adalah penggunaan memori yang lebih besar karena setiap node harus menyimpan dua pointer sekaligus.
## Guided
### soal 1 
```c++
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* prev;
    Node* next;
};

Node* head = nullptr;
Node* tail = nullptr;

void insertDepan(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->prev = nullptr;
    newNode->next = head;

    if (head != nullptr)
       head->prev = newNode;
    else
       tail = newNode;

    head = newNode;
    cout << "Data " << data << " berhasil ditambahkan di depan. \n";
}

void insertBelakang(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    newNode->prev = tail;

    if (tail != nullptr)
        tail->next = newNode;
    else
        head = newNode;

    tail = newNode;
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

void insertSetelah(int target, int data) {
    Node* current = head;
    while (current != nullptr && current ->data != target)
        current = current->next;

    if(current == nullptr) {
        cout << "Data " << target << " tidak ditemukan.\n";
        return;
    }

    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = current->next;
    newNode->prev = current;

    if (current->next != nullptr)
        current->next->prev = newNode;
    else
        tail = newNode;

    current->next = newNode;
    cout << "Data " << data << " berhasil disisipkan setelah " << target << ".\n";
}

void hapusDepan() {
    if (head == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    Node* temp = head;
    head = head->next;

    if (head != nullptr)
        head->prev = nullptr;
    else
        tail = nullptr;

    cout << "Data " << temp->data << " dihapus dari depan.\n";
    delete temp;
}

void hapusBelakang() {
    if  (tail == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    Node* temp = tail;
    tail = tail->prev;

    if (tail != nullptr)
        tail->next = nullptr;
    else
        head = nullptr;
    
    cout << "Data " << temp->data << " dihapus dari belakang.\n";
    delete temp;
}

void hapusData(int target) {
    Node* current = head;
    while (current != nullptr && current->data != target)
        current = current->next;

    if (current == nullptr) {
        cout << "Data " << target << " tidak ditemukan.\n";
        return;
    }

    if (current == head)
        hapusDepan();
    else if (current == tail)
        hapusBelakang();
    else {
        current->prev->next = current->next;
        current->next->prev = current->prev;
        cout << "Data " << target << " dihapus.\n";
        delete current;
    }
}
void updateData(int oldData, int newData) {
    Node* current = head;
    while (current != nullptr && current->data != oldData)
        current = current->next;

    if (current == nullptr) {
        cout << "Data " << oldData << " tidak ditemukan.\n";
        return;
    }

    current->data = newData;
    cout << "Data " << oldData << " diubah menjadi " << newData << ".\n";
}
void tampilDepan() {
    if (head == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari depan): ";
    Node* current = head;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->next;
    }
    cout << "\n";
}

// ====================================
// Fungsi: Tampilkan dari belakang
// ====================================
void tampilBelakang() {
    if (tail == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari belakang): ";
    Node* current = tail;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->prev;
    }
    cout << "\n";
}

// ====================================
// MAIN PROGRAM (MENU INTERAKTIF)
// ====================================
int main() {
    int pilihan, data, target, oldData, newData;

    do {
        cout << "\n===== MENU DOUBLE LINKED LIST =====\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah Data\n";
        cout << "4. Hapus Depan\n";
        cout << "5. Hapus Belakang\n";
        cout << "6. Hapus Data Tertentu\n";
        cout << "7. Update Data\n";
        cout << "8. Tampil dari Depan\n";
        cout << "9. Tampil dari Belakang\n";
        cout << "0. Keluar\n";
        cout << "===================================\n";
        cout << "Pilih menu: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "Masukkan data: ";
                cin >> data;
                insertDepan(data);
                break;
            case 2:
                cout << "Masukkan data: ";
                cin >> data;
                insertBelakang(data);
                break;
            case 3:
                cout << "Masukkan data target: ";
                cin >> target;
                cout << "Masukkan data baru: ";
                cin >> data;
                insertSetelah(target, data);
                break;
            case 4:
                hapusDepan();
                break;
            case 5:
                hapusBelakang();
                break;
            case 6:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> target;
                hapusData(target);
                break;
            case 7:
                cout << "Masukkan data lama: ";
                cin >> oldData;
                cout << "Masukkan data baru: ";
                cin >> newData;
                updateData(oldData, newData);
                break;
            case 8:
                tampilDepan();
                break;
            case 9:
                tampilBelakang();
                break;
            case 0:
                cout << "👋 Keluar dari program.\n";
                break;
            default:
                cout << "Pilihan tidak valid.\n";
        }

    } while (pilihan != 0);

    return 0;
}

```
Program diatas merupakan implementasi dari struktur data double linked list menggunakan bahasa c++ yang memungkinkan penyimpanan data secara dinamis dan dapat diakses dua arah program memiliki node yang berisi data pointer prev untuk menunjuk node sebelumnya dan next untuk menunjuk node berikutnya terdapat fungsi untuk menambah data di depan belakang dan setelah data tertentu serta fungsi untuk menghapus data baik di depan belakang maupun berdasarkan nilai tertentu selain itu ada juga fungsi update untuk mengubah nilai data dan dua fungsi tampil untuk menampilkan isi list dari depan maupun dari belakang program dilengkapi menu interaktif di fungsi main agar pengguna bisa memilih operasi yang diinginkan seperti menambah menghapus mengupdate dan menampilkan data secara langsung melalui input terminal


> Output


## Unguided

### Soal 1
Buatlah ADT Doubly Linked list sebagai berikut di dalam file “Doublylist.h”:

```go
Type infotype : kendaraan <
    nopol : string
    warna : string
    thnBuat : integer
>
Type address : pointer to ElmList
Type ElmList <
    info : infotype
    next : address
    prev : address
>

Type List <
    First : address
    Last : address
>

procedure CreateList( input/output L : List )
function alokasi( x : infotype ) → address
procedure dealokasi(input/output P : address )
procedure printInfo( input L : List )
procedure insertLast(input/output L : List,  
   input P : address )
```
Buatlah implementasi ADT Doubly Linked list pada file “Doublylist.cpp” dan coba hasil implementasi ADT pada file “main.cpp”.

> Contoh Output:
``` Output
masukkan nomor polisi: D001
masukkan warna kendaraan: hitam
masukkan tahun kendaraan: 90
masukkan nomor polisi: D003
masukkan warna kendaraan: putih
masukkan tahun kendaraan: 70
masukkan nomor polisi: D001
masukkan warna kendaraan: merah
masukkan tahun kendaraan: 80
nomor polisi sudah terdaftar
masukkan nomor polisi: D004
masukkan warna kendaraan: kuning
masukkan tahun kendaraan: 90
DATA LIST 1
no polisi : D004
warna     : kuning
tahun     : 90
no polisi : D003
warna     : putih
tahun     : 70
no polisi : D001
warna     : hitam
tahun     : 90
```

## doublylist.h
```go
#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H

#include <iostream>
using namespace std;

struct Kendaraan {
    string nopol;
    string warna;
    int tahun;
    Kendaraan* next;
    Kendaraan* prev;
};

Kendaraan* createNode(string nopol, string warna, int tahun);
void insertLast(Kendaraan*& head, Kendaraan* nodeBaru);
void showList(Kendaraan* head);
Kendaraan* findNode(Kendaraan* head, string nopol);
void deleteAfter(Kendaraan* prec, Kendaraan*& hapus);
void deleteLast(Kendaraan*& head, Kendaraan*& hapus);
void deleteNode(Kendaraan*& node);

#endif

```

## doublylist.cpp
```go
#include "doublylist.h"

Kendaraan* createNode(string nopol, string warna, int tahun) {
    Kendaraan* baru = new Kendaraan();
    baru->nopol = nopol;
    baru->warna = warna;
    baru->tahun = tahun;
    baru->next = nullptr;
    baru->prev = nullptr;
    return baru;
}

void insertLast(Kendaraan*& head, Kendaraan* nodeBaru) {
    if (head == nullptr) {
        head = nodeBaru;
    } else {
        Kendaraan* temp = head;
        while (temp->next != nullptr) temp = temp->next;
        temp->next = nodeBaru;
        nodeBaru->prev = temp;
    }
}

void showList(Kendaraan* head) {
    Kendaraan* temp = head;
    while (temp != nullptr) {
        cout << temp->nopol << " | " << temp->warna << " | " << temp->tahun << endl;
        temp = temp->next;
    }
    cout << endl;
}

Kendaraan* findNode(Kendaraan* head, string nopol) {
    Kendaraan* temp = head;
    while (temp != nullptr && temp->nopol != nopol) {
        temp = temp->next;
    }
    return temp;
}

void deleteAfter(Kendaraan* prec, Kendaraan*& hapus) {
    if (prec != nullptr && prec->next != nullptr) {
        hapus = prec->next;
        prec->next = hapus->next;
        if (hapus->next != nullptr)
            hapus->next->prev = prec;
    } else {
        hapus = nullptr;
    }
}

void deleteLast(Kendaraan*& head, Kendaraan*& hapus) {
    if (head == nullptr) {
        hapus = nullptr;
        return;
    }
    if (head->next == nullptr) {
        hapus = head;
        head = nullptr;
    } else {
        Kendaraan* temp = head;
        while (temp->next->next != nullptr)
            temp = temp->next;
        hapus = temp->next;
        temp->next = nullptr;
    }
}

void deleteNode(Kendaraan*& node) {
    delete node;
    node = nullptr;
}

```
## main.cpp
```go
#include "doublylist.h"

int main() {
    Kendaraan* kendaraanList = nullptr;

    insertLast(kendaraanList, createNode("D001", "Kuning", 2020));
    insertLast(kendaraanList, createNode("D002", "Putih", 2018));
    insertLast(kendaraanList, createNode("D003", "Kuning", 2021));
    insertLast(kendaraanList, createNode("D004", "Putih", 2021));

    showList(kendaraanList);

    cout << "=== Hapus Setelah D002 ===\n";
    Kendaraan* prec = findNode(kendaraanList, "D002");
    Kendaraan* hapus = nullptr;
    deleteAfter(prec, hapus);
    if (hapus != nullptr) {
        cout << "Menghapus setelah D002: " << hapus->nopol << endl;
        deleteNode(hapus);
    }

    showList(kendaraanList);

    cout << "=== Hapus Elemen Terakhir ===\n";
    deleteLast(kendaraanList, hapus);
    if (hapus != nullptr) {
        cout << "Menghapus: " << hapus->nopol << endl;
        deleteNode(hapus);
    }

    showList(kendaraanList);

    return 0;
}

```
> Output
> ![Screenshot bagian x](ssunguidedmodul6.png)
Program ini merupakan implementasi Doubly Linked List dalam bahasa C++ untuk mengelola data kendaraan yang terdiri dari nomor polisi, warna (kuning atau putih), dan tahun pembuatan. Setiap node dalam list memiliki dua pointer, yaitu next untuk menunjuk ke node berikutnya dan prev untuk menunjuk ke node sebelumnya, sehingga memungkinkan traversal dua arah. Program ini menyediakan berbagai fungsi seperti insertLast() untuk menambah data kendaraan di akhir list, findNode() untuk mencari kendaraan berdasarkan nomor polisi, serta deleteAfter() dan deleteLast() untuk menghapus node tertentu. Di fungsi main(), beberapa data kendaraan dimasukkan ke dalam list, kemudian ditampilkan, lalu dilakukan penghapusan node setelah kendaraan dengan nomor “D002” dan juga penghapusan elemen terakhir. Setelah setiap operasi, daftar kendaraan ditampilkan kembali untuk memperlihatkan hasil perubahan.

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
