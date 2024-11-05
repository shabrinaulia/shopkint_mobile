# Shopkint
**Nama : Shabrina Aulia Kinanti**
**NPM : 2306245472**
**Kelas : B**

A new Flutter project.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.



## **Penjelasan Tugas**
<details>
<summary> <b> Tugas 7 : Elemen Dasar Django </b> </summary>

## **Checklist Tugas**

## **Jelaskan apa yang dimaksud dengan stateless widget dan stateful widget, dan jelaskan perbedaan dari keduanya.**
- StatelessWidget adalah widget yang tidak memiliki state yang dapat berubah setelah widget tersebut dibuat. Artinya, widget ini bersifat statis atau tidak dapat berubah selama aplikasi berjalan, kecuali jika direbuild atau dibangun ulang secara manual oleh program.
1. Tidak punya state yang bisa berubah.
2. Cocok untuk UI statis (tidak berubah).
3. Contoh: Teks, ikon statis.
4. Tidak bisa diperbarui tanpa rebuild seluruh widget. 
5. UI statis, tidak berubah.

- StatefulWidget adalah widget yang memiliki state yang dapat berubah selama siklus hidup widget tersebut. Artinya, widget ini dapat memperbarui atau mengubah tampilannya secara dinamis saat aplikasi berjalan berdasarkan interaksi pengguna atau perubahan data.
1. Punya state yang bisa berubah.
2. Cocok untuk UI dinamis (berubah seiring interaksi).
3. Contoh: Tombol yang berubah warna saat ditekan, counter.
4. Menggunakan setState untuk memperbarui tampilan.
5. UI dinamis, bisa berubah selama aplikasi berjalan.

## **Apa fungsi dari setState()? Jelaskan variabel apa saja yang dapat terdampak dengan fungsi tersebut.**
`setState()` digunakan untuk memperbarui UI saat ada perubahan data pada widget `Stateful`. Dengan memanggil `setState()`, Flutter akan membangun ulang (re-render) bagian UI yang terkait, sehingga tampilan sesuai dengan data terbaru.

Variabel yang Terpengaruh:
- Variabel dalam State : Semua variabel yang didefinisikan di kelas `State` dari widget, seperti `int counter`, `bool`, `String`, atau `List` yang digunakan di `build()`.
Intinya, `setState()` membuat Flutter tahu bahwa ada data yang berubah dan perlu diperbarui di layar.

## **Jelaskan perbedaan antara const dengan final.**
const: Nilai tetap pada compile-time (wajib diketahui saat kompilasi).
- Digunakan untuk nilai tetap yang sudah diketahui sejak kompilasi (compile-time constant).
- Objek yang dideklarasikan dengan const adalah immutable (tidak dapat diubah) dan dibuat hanya sekali di memori.
- Biasanya digunakan untuk nilai yang benar-benar konstan seperti angka tetap, string tetap, atau objek yang bisa dipastikan nilainya tidak akan berubah.

final: Nilai tetap pada runtime, bisa ditentukan saat program berjalan.
- Digunakan untuk nilai yang hanya bisa ditetapkan satu kali dan tidak bisa diubah setelah ditetapkan.
- Nilainya bisa ditentukan saat runtime, bukan hanya saat kompilasi.
- Cocok untuk nilai yang bisa berubah-ubah namun hanya perlu diinisialisasi sekali.

## **Jelaskan bagaimana cara kamu mengimplementasikan checklist-checklist di atas.**
* ### Membuat sebuah program Flutter 
1. Membuat folder baru bernama shopkint_mobile
2. buka terminal dan tulis prompt seperti dibawah ini
```
flutter create shokint
cd shopkint
```
3. Jalankan dengan `flutter run`

* ### Membuat tiga tombol sederhana dengan ikon dan teks
1. Buat file baru di folder lib bernama `menu.dart` lalu pindahkan isi dari `main.dart` baris ke 39-kebawah dan tambahkan `import 'package:flutter/material.dart';`lalu tambahkan code `home: const MyHomePage(title: 'Flutter Demo Home Page'),` di `main.dart`
2. Membuat class di `menu.dart` untuk card info yang berisi nama, NPM, kelas
```
class InfoCard extends StatelessWidget {
  final String title;
  final String content;

  const InfoCard({super.key, required this.title, required this.content});

  @override
  Widget build(BuildContext context) {
    return Card(
      elevation: 2.0,
      child: Container(
        width: MediaQuery.of(context).size.width / 3.5,
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            Text(
              title,
              style: const TextStyle(fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 8.0),
            Text(content),
          ],
        ),
      ),
    );
  }
}
```
3. Membuat class baru yaitu `ItemHomePage` yang berisi nama dan icon di file `menu.dart`
```
class ItemHomepage {
  final String name;
  final IconData icon;
  final Color color;

  ItemHomepage(this.name, this.icon, this.color);
}
``` 
dan setelah itu tambahkan code dibawah ini untuk membuat list tombol yang ada di homepage nya dan button dengan warna yang berbeda
```
final List<ItemHomepage> items = [
    ItemHomepage("Lihat Daftar Product", Icons.shopping_cart, Color(0xFF795548)), // Medium-light brown
    ItemHomepage("Tambah Product", Icons.add, Color(0xFF8D6E63)), // Medium brown
    ItemHomepage("Logout", Icons.logout, Color(0xFF8B5E5E)), // Muted reddish-brown for Logout
  ];
```
* ###  Memunculkan Snackbar
1. di `menu.dart` tambahkan class dibawah ini sehingga jika tombol dipencek dia menampilkan snackbar yang sesuai dengan tombolnya
```
class ItemHomepage {
  final String name;
  final IconData icon;
  final Color color;

  ItemHomepage(this.name, this.icon, this.color);
}

class ItemCard extends StatelessWidget {
  final ItemHomepage item;
  
  const ItemCard(this.item, {super.key}); 

  @override
  Widget build(BuildContext context) {
    return Material(
      color: item.color, // Use the item's color for background
      borderRadius: BorderRadius.circular(12),
      child: InkWell(
        onTap: () {
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(
              SnackBar(content: Text("Kamu telah menekan tombol ${item.name}!"))
            );
        },
        child: Container(
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

</details># shopkint_mobile
