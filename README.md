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


# shopkint_mobile

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

</details>

<details>
<summary> <b> Tugas 8 : Elemen Dasar Django </b> </summary>

## **Checklist Tugas**

## **Apa kegunaan const di Flutter? Jelaskan apa keuntungan ketika menggunakan const pada kode Flutter. Kapan sebaiknya kita menggunakan const, dan kapan sebaiknya tidak digunakan?.**
Kegunaan: const di Flutter digunakan untuk membuat nilai atau widget menjadi konstan. Artinya, nilai tersebut tidak akan berubah sepanjang runtime aplikasi dan akan disimpan di dalam memori secara tetap. const memungkinkan Flutter menghindari pembuatan ulang objek yang sama setiap kali widget dibangun kembali.
Keuntungan: 
- Mengurangi penggunaan memori karena objek const hanya diinisialisasi satu kali dan tidak berubah.
- Meningkatkan efisiensi performa karena Flutter tidak perlu melakukan rebuild pada objek yang sudah bersifat konstan.
Const sebaiknya digunakan saat membuat widget atau nilai yang tidak perlu diubah sepanjang runtime aplikasi, seperti widget statis (misalnya, teks label atau ikon yang tidak berubah).

## **Jelaskan dan bandingkan penggunaan Column dan Row pada Flutter. Berikan contoh implementasi dari masing-masing layout widget ini!**
Column: Column adalah widget yang menata widget-widget anaknya dalam susunan vertikal (atas ke bawah). Contoh penggunaannya adalah untuk menumpuk widget secara vertikal, seperti membuat daftar teks atau gambar dalam satu kolom.
```
Column(
  mainAxisAlignment: MainAxisAlignment.center,
  crossAxisAlignment: CrossAxisAlignment.start,
  children: [
    Text('Item 1'),
    Text('Item 2'),
    Text('Item 3'),
  ],
)
```
Row: Row adalah widget yang menata widget-widget anaknya dalam susunan horizontal (kiri ke kanan). Contohnya adalah membuat baris ikon atau tombol secara horizontal.
```
Row(
  mainAxisAlignment: MainAxisAlignment.spaceAround,
  children: [
    Icon(Icons.home),
    Icon(Icons.star),
    Icon(Icons.person),
  ],
)
```
Perbandingan :
- Column cocok digunakan saat ingin menampilkan widget secara vertikal, sedangkan Row untuk horizontal.
- Column dan Row memiliki properti mainAxisAlignment dan crossAxisAlignment untuk mengatur posisi widget anak.
- Keduanya digunakan dalam tata letak yang berbeda tergantung pada orientasi widget yang diinginkan.

## **Sebutkan apa saja elemen input yang kamu gunakan pada halaman form yang kamu buat pada tugas kali ini. Apakah terdapat elemen input Flutter lain yang tidak kamu gunakan pada tugas ini? Jelaskan!**
Elemen yang digunakan :
1. TextFormField untuk memasukkan teks, seperti nama produk, harga, deskripsi, rating, dan URL gambar.

Yang tidak digunakan :
1. Checkbox: Untuk pilihan biner, misalnya untuk menandai pilihan sebagai aktif atau tidak.
2. Switch: Untuk toggle on/off status tertentu.
3. Slider: Untuk memilih nilai dalam rentang tertentu.
4. DropdownButton: Untuk pilihan dari daftar item.
Alasan Tidak Digunakan: Elemen input seperti Checkbox, Switch, atau DropdownButton tidak digunakan karena tidak sesuai dengan kebutuhan form ini, yang lebih berfokus pada masukan teks dan angka sederhana.

## **Bagaimana cara kamu mengatur tema (theme) dalam aplikasi Flutter agar aplikasi yang dibuat konsisten? Apakah kamu mengimplementasikan tema pada aplikasi yang kamu buat?**
Dalam Flutter, tema dapat diatur pada level MaterialApp menggunakan properti theme dan darkTheme. Kita bisa menggunakan ThemeData untuk menentukan warna utama, warna latar belakang, font, dan elemen lain yang membuat tampilan aplikasi konsisten.

Ya, saya menggunakan tema pada aplikasinya. Tema diatur menggunakan properti ThemeData pada widget MaterialApp di main.dart. Dalam ThemeData, color scheme dibuat dari ColorScheme.fromSwatch dengan primarySwatch: Colors.brown. Kemudian, warna primary dan secondary diatur menggunakan warna coklat muda dan coklat sedikit lebih gelap untuk memastikan konsistensi warna di seluruh aplikasi.
```
theme: ThemeData(
  colorScheme: ColorScheme.fromSwatch(
    primarySwatch: Colors.brown,
  ).copyWith(
    primary: Colors.brown[200], // Light brown for primary color
    secondary: Colors.brown[300], // Slightly darker light brown for secondary color
  ),
),
```

## **Bagaimana cara kamu menangani navigasi dalam aplikasi dengan banyak halaman pada Flutter?**
Pada kode ini, halaman home diatur sebagai MyHomePage() di dalam MaterialApp. Dalam aplikasi dengan banyak halaman, Navigator akan digunakan untuk mengelola perpindahan halaman. `Navigator.push` atau `Navigator.pushReplacement` biasanya digunakan untuk berpindah dari satu halaman ke halaman lain, seperti dalam kasus ini ketika membuka halaman menu.
Implementasi Navigasi: Pada halaman MyHomePage atau halaman lain, kita dapat menggunakan Navigator.push atau Navigator.pushReplacement untuk membuka halaman Menu atau halaman lain yang diinginkan. Contoh penggunaan :
```
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => MenuScreen()),
);
```

</details>
