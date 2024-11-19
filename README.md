# Shopkint
**Nama:** Shabrina Aulia Kinanti  
**NPM:** 2306245472  
**Kelas:** B

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

## **Jelaskan mengapa kita perlu membuat model untuk melakukan pengambilan ataupun pengiriman data JSON? Apakah akan terjadi error jika kita tidak membuat model terlebih dahulu?**
Membuat model untuk data JSON penting karena:
- Struktur dan validasi: Model membantu menjaga struktur data yang konsisten. JSON yang diterima dari server mungkin memiliki struktur kompleks yang sulit dikelola tanpa model.
- Pemrosesan yang mudah: Dengan model, data JSON dapat dengan mudah diubah menjadi objek Dart untuk memanipulasi dan menampilkannya.
- Error minimization: Model membantu mendeteksi kesalahan pada tahap awal, seperti ketika ada properti yang hilang atau tipe data yang salah.
- Efisiensi kode: Model mempermudah pengelolaan data dengan menyediakan fungsi seperti serialisasi/deserialisasi.

jika kita tidak membuat model terlebih dahulu :
- Tidak akan langsung terjadi error, tetapi data JSON perlu diakses secara manual menggunakan peta (map) yang membuat kode sulit dibaca dan rentan terhadap kesalahan seperti null-pointer exceptions.
- Pemeliharaan aplikasi menjadi lebih sulit karena pengubahan struktur data di server memerlukan banyak penyesuaian manual di kode.

## **Jelaskan fungsi dari library http yang sudah kamu implementasikan pada tugas ini**
Library http di Flutter digunakan untuk melakukan komunikasi HTTP, baik untuk pengambilan (GET) maupun pengiriman (POST) data ke server. Fungsi utamanya:

- Mengirim request: Mendukung metode HTTP seperti GET, POST, PUT, DELETE, dll.
- Menerima response: Mengelola data dari server, termasuk decoding JSON untuk digunakan dalam aplikasi.
- Otentikasi: Mendukung header custom untuk otorisasi (seperti token).

## **Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.**
Fungsi `CookieRequest`:
- Mengelola cookie untuk otentikasi dan sesi pengguna.
- Menyimpan cookie yang diterima dari server untuk digunakan dalam request berikutnya.
- Mempermudah otentikasi dengan server tanpa perlu memasukkan kembali kredensial.

Mengapa instance dibagikan:
- Instance yang sama memastikan sesi konsisten di seluruh aplikasi.
- Memungkinkan setiap komponen mengakses data sesi tanpa membuat ulang koneksi.
- Meningkatkan efisiensi dengan berbagi data (seperti status login) antar widget.

## **JJelaskan mekanisme pengiriman data mulai dari input hingga dapat ditampilkan pada Flutter.**
a. Input Data di Flutter
Widget Input: Data diambil dari input seperti TextField atau Form.
```
final TextEditingController _nameController = TextEditingController();
final TextEditingController _priceController = TextEditingController();
```
b. Data Dikirim ke Server
Request HTTP POST:
Data dari controller diambil, dikonversi menjadi JSON, dan dikirimkan ke server.
```
final response = await request.postJson(
  'http://127.0.0.1:8000/api/products/',
  jsonEncode({
    'name': _nameController.text,
    'price': double.parse(_priceController.text),
  }),
);
```
server menerima respon JSON dan mevalidasi data
c. Data Disimpan di Database
Django memproses data dan menyimpannya di database melalui model.
```
@csrf_exempt
def create_product(request):
    if request.method == 'POST':
        data = json.loads(request.body)
        product = Product.objects.create(name=data['name'], price=data['price'])
        product.save()
        return JsonResponse({'status': 'success', 'message': 'Product created successfully!'})
```
d. Data Diambil oleh Flutter
Request HTTP GET:
Flutter mengirimkan GET request untuk mengambil data dari server.
```
final response = await request.get('http://127.0.0.1:8000/api/products/');
final List<Product> products = (jsonDecode(response.body) as List)
    .map((data) => Product.fromJson(data))
    .toList();
```
Server mengembalikan data dalam format JSON.
e. Data Ditampilkan di Flutter
Menggunakan widget seperti ListView atau FutureBuilder:
```
ListView.builder(
  itemCount: products.length,
  itemBuilder: (context, index) {
    return ListTile(
      title: Text(products[index].name),
      subtitle: Text('Price: ${products[index].price}'),
    );
  },
);
```
## **Jelaskan mekanisme autentikasi dari login, register, hingga logout. Mulai dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.**
a. Login
1. Flutter:
- Input username dan password melalui TextField.
- Flutter mengirim POST request ke endpoint /auth/login/ dengan data:
```
{
  "username": "admin",
  "password": "admin123"
}
```
2. Django:
- Django memproses data dengan authenticate dan memeriksa username serta password
```
user = authenticate(username=username, password=password)
if user is not None:
    login(request, user)
    return JsonResponse({'status': True, 'message': 'Login sukses!'})
else:
    return JsonResponse({'status': False, 'message': 'Login gagal!'})
```
3. Response ke Flutter:
Jika berhasil, Django mengembalikan status True dan cookie sesi.
Flutter menyimpan cookie melalui CookieRequest.
4. Navigasi ke Menu:
Jika login berhasil, navigasikan pengguna ke halaman utama menggunakan Navigator.

b. Register
1. Flutter:
Data username dan password dikirim ke endpoint `/auth/register/`.
2. Django:

Data diverifikasi, dan akun baru dibuat:
```
user = User.objects.create_user(username=username, password=password)
```
3. Response ke Flutter:
- Django mengembalikan status sukses jika pembuatan akun berhasil.
- Flutter menampilkan pesan sukses atau error.

c. Logout
1. Flutter:
Mengirim POST request ke endpoint /auth/logout/.
```
final response = await request.logout('http://127.0.0.1:8000/auth/logout/');
```
2. Django:
Django menghapus sesi pengguna:
```
auth_logout(request)
return JsonResponse({'status': True, 'message': 'Logout berhasil!'})
```
3. Navigasi ke Login:
Jika logout berhasil, Flutter mengarahkan pengguna kembali ke halaman login.

## **Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step! (bukan hanya sekadar mengikuti tutorial).**
* ### Setup Autentikasi pada Django untuk Flutter
1. Membuat Django App Authentication pada proyek django Shopkint
2. Tambahkan `authentication`, `corsheaders` ke `INSTALLED_APPS` pada shopkint `settings.py`
3. Jalankan perintah `pip install django-cors-headers` dan menambahkan `django-cors-headers` ke `requirements.txt`.
4. Tambahkan `corsheaders.middleware.CorsMiddleware` ke `MIDDLEWARE` pada shopkint settings.py
5. Tambahkan beberapa variabel di `settings.py`
```
CORS_ALLOW_ALL_ORIGINS = True
CORS_ALLOW_CREDENTIALS = True
CSRF_COOKIE_SECURE = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SAMESITE = 'None'
SESSION_COOKIE_SAMESITE = 'None'
```

* ### Step 1: Mengimplementasikan Fitur Registrasi Akun
1. Tambahkan view untuk register di `authentication/views.py`
```
from django.contrib.auth.models import User
from django.http import JsonResponse
import json
from django.views.decorators.csrf import csrf_exempt

@csrf_exempt
def register(request):
    if request.method == 'POST':
        data = json.loads(request.body)
        username = data['username']
        password1 = data['password1']
        password2 = data['password2']

        if password1 != password2:
            return JsonResponse({"status": False, "message": "Passwords do not match."}, status=400)
        
        if User.objects.filter(username=username).exists():
            return JsonResponse({"status": False, "message": "Username already exists."}, status=400)

        user = User.objects.create_user(username=username, password=password1)
        user.save()

        return JsonResponse({"status": True, "message": "User registered successfully!"})
```

2. Tambahkan URL di authentication/urls.py:
```
from .views import register
urlpatterns = [
    path('register/', register, name='register'),
]
```

3. Tambahkan file `register.dart` di `lib/screens`:
```
ElevatedButton(
  onPressed: () async {
    String username = _usernameController.text;
    String password1 = _passwordController.text;
    String password2 = _confirmPasswordController.text;

    final response = await request.postJson(
        "http://127.0.0.1:8000/auth/register/",
        jsonEncode({"username": username, "password1": password1, "password2": password2}));
    if (response['status'] == 'success') {
      ScaffoldMessenger.of(context).showSnackBar(SnackBar(content: Text('Successfully registered!')));
    } else {
      ScaffoldMessenger.of(context).showSnackBar(SnackBar(content: Text('Failed to register!')));
    }
  },
  child: const Text('Register'),
);
```

* ### Step 2: Membuat Halaman Login
1. Tambahkan view login di authentication/views.py dan jangan lupa sambungkan url nya 
```
from django.contrib.auth import authenticate, login
@csrf_exempt
def login_view(request):
    username = request.POST.get('username')
    password = request.POST.get('password')
    user = authenticate(username=username, password=password)
    if user is not None:
        login(request, user)
        return JsonResponse({"status": True, "message": "Login successful!"})
    return JsonResponse({"status": False, "message": "Invalid credentials."})
```
2. Tambahkan file login.dart di lib/screens
```
ElevatedButton(
  onPressed: () async {
    String username = _usernameController.text;
    String password = _passwordController.text;

    final response = await request.login(
        "http://127.0.0.1:8000/auth/login/",
        {"username": username, "password": password});
    if (response['status'] == true) {
      Navigator.pushReplacement(context, MaterialPageRoute(builder: (_) => HomePage()));
    } else {
      ScaffoldMessenger.of(context).showSnackBar(SnackBar(content: Text('Login failed!')));
    }
  },
  child: const Text('Login'),
);
```

* ### Step 3: Integrasikan Sistem Autentikasi Django dengan Flutter
1. Tambahkan Library pbp_django_auth
```
flutter pub add pbp_django_auth
flutter pub add provider
```
2. Setup CookieRequest di main.dart
```
return Provider(
  create: (_) => CookieRequest(),
  child: MaterialApp(
    home: const LoginPage(),
  ),
);
```

* ### Step 4: Membuat Model Kustom
1. Salin respons JSON dari Django.
2. Gunakan Quicktype untuk mengonversi ke kode Dart.
3. Buat file product_entry.dart di lib/models dan salin kode dart
```
import 'dart:convert';

List<ProductEntry> productEntryFromJson(String str) => List<ProductEntry>.from(json.decode(str).map((x) => ProductEntry.fromJson(x)));

String productEntryToJson(List<ProductEntry> data) => json.encode(List<dynamic>.from(data.map((x) => x.toJson())));

class ProductEntry {
    String model;
    String pk;
    Fields fields;

    ProductEntry({
        required this.model,
        required this.pk,
        required this.fields,
    });

    factory ProductEntry.fromJson(Map<String, dynamic> json) => ProductEntry(
        model: json["model"],
        pk: json["pk"],
        fields: Fields.fromJson(json["fields"]),
    );

    Map<String, dynamic> toJson() => {
        "model": model,
        "pk": pk,
        "fields": fields.toJson(),
    };
}

class Fields {
    int user;
    String productName;
    int price;
    String description;
    int rating;
    String image;

    Fields({
        required this.user,
        required this.productName,
        required this.price,
        required this.description,
        required this.rating,
        required this.image,
    });

    factory Fields.fromJson(Map<String, dynamic> json) => Fields(
        user: json["user"],
        productName: json["product_name"],
        price: json["price"],
        description: json["description"],
        rating: json["rating"],
        image: json["image"],
    );

    Map<String, dynamic> toJson() => {
        "user": user,
        "product_name": productName,
        "price": price,
        "description": description,
        "rating": rating,
        "image": image,
    };
}
```

* ### Step 5: Membuat Halaman Daftar Item
1. Buat Halaman untuk Fetch Data:
- Tambahkan file list_productentry.dart di lib/screens
```
class _ProductEntryPageState extends State<ProductEntryPage> {
  Future<List<ProductEntry>> fetchProducts(CookieRequest request) async {
    try {
      // Gunakan URL yang sesuai (http://10.0.2.2:8000/json/ untuk emulator Android)
      final response = await request.get('http://127.0.0.1:8000/json/');

      // Validasi respons
      if (response == null || response.isEmpty) {
        throw Exception('No data available or failed to fetch data');
      }

      List<ProductEntry> productList = [];
      for (var d in response) {
        productList.add(ProductEntry.fromJson(d));
      }
      return productList;
    } catch (e) {
      // Tangani error
      print("Error: $e");
      return [];
    }
  }
```
2. Tampilkan Data:
```
@override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();
    return Scaffold(
      appBar: AppBar(
        title: const Text(
          'Product List',
          style: TextStyle(
            color: Colors.white, // Change the text color to brown
          ),
        ),
        backgroundColor: Theme.of(context).colorScheme.primary,
        foregroundColor: Colors.white,
      ),
      drawer: const LeftDrawer(),
      body: FutureBuilder(
        future: fetchProducts(request),
        builder: (context, AsyncSnapshot snapshot) {
          if (snapshot.connectionState == ConnectionState.waiting) {
            return const Center(child: CircularProgressIndicator());
          } else if (snapshot.hasError) {
            return Center(
              child: Text(
                'Error: ${snapshot.error}',
                style: const TextStyle(color: Colors.red),
              ),
            );
          } else if (!snapshot.hasData || snapshot.data.isEmpty) {
            return const Center(
              child: Text('No products available.'),
            );
          } else {
            return ListView.builder(
              itemCount: snapshot.data.length,
              itemBuilder: (_, index) {
                final product = snapshot.data[index];
                return GestureDetector(
                  onTap: () {
                    Navigator.push(
                      context,
                      MaterialPageRoute(
                        builder: (context) => DetailProductEntry(product: product),
                      ),
                    );
                  },
                  child: Container(
                    margin: const EdgeInsets.symmetric(horizontal: 16, vertical: 12),
                    padding: const EdgeInsets.all(20.0),
                    decoration: BoxDecoration(
                      color: Colors.white,
                      borderRadius: BorderRadius.circular(10.0),
                      boxShadow: const [
                        BoxShadow(
                          color: Colors.black12,
                          blurRadius: 4.0,
                          offset: Offset(0, 4),
                        ),
                      ],
                    ),
                    child: Column(
                      crossAxisAlignment: CrossAxisAlignment.start,
                      children: [
                        Center(
                          child: Text(
                            (product.fields.productName),
                            style: const TextStyle(
                              fontSize: 24.0,
                              fontWeight: FontWeight.bold,
                              color: Colors.brown,
                            ),
                            textAlign: TextAlign.center,
                          ),
                        ),
                        const SizedBox(height: 10),
                        Text("Price: Rp${product.fields.price}"),
                        const SizedBox(height: 10),
                        Text("Description: ${product.fields.description}"),
                        const SizedBox(height: 10),
                        Text("Rating: ${product.fields.rating}"),
                      ],
                    ),
                  ),
                );
              },
            );
          }
        },
      ),
    );
  }
```

* ### Step 6: Membuat Halaman Detail Item
1. Buat file detail_productentry.dart di lib/screens
```
import 'package:flutter/material.dart';
import 'package:shopkint/models/product_entry.dart';

class DetailProductEntry extends StatelessWidget {
  final ProductEntry product;

  const DetailProductEntry({Key? key, required this.product}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text(
          'Detail Product',
          style: TextStyle(
            color: Colors.white, // Warna teks di AppBar
          ),
        ),
        backgroundColor: Theme.of(context).colorScheme.primary,
        foregroundColor: Colors.white,
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: SingleChildScrollView(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Center(
                child: Text(
                  product.fields.productName,
                  style: const TextStyle(
                    fontSize: 24,
                    fontWeight: FontWeight.bold,
                    color: Colors.brown,
                  ),
                ),
              ),
              const SizedBox(height: 20),
              Text(
                'Price: Rp${product.fields.price}',
                style: const TextStyle(fontSize: 18),
              ),
              const SizedBox(height: 10),
              Text(
                'Description: ${product.fields.description}',
                style: const TextStyle(fontSize: 18),
              ),
              const SizedBox(height: 10),
              Text(
                'Rating: ${product.fields.rating}',
                style: const TextStyle(fontSize: 18),
              ),
              const SizedBox(height: 20),
              Center(
                child: ElevatedButton(
                  onPressed: () {
                    Navigator.pop(context);
                  },
                  child: const Text('Back to List'),
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

* ### Step 7 :Integrasi Form Flutter Dengan Layanan Django
1. Membuat sebuah fungsi view baru pada main/views.py aplikasi Django
```
@csrf_exempt
def create_mood_flutter(request):
    if request.method == 'POST':

        data = json.loads(request.body)
        new_mood = MoodEntry.objects.create(
            user=request.user,
            mood=data["mood"],
            mood_intensity=int(data["mood_intensity"]),
            feelings=data["feelings"]
        )

        new_mood.save()

        return JsonResponse({"status": "success"}, status=200)
    else:
        return JsonResponse({"status": "error"}, status=401)
```
2. Tambahkan path urls nya `path('create-flutter/', create_mood_flutter, name='create_mood_flutter'),`
3. Hubungkan halaman productentry_form.dart dengan CookieRequest 
```
@override
Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();

    return Scaffold(
    )
}
```
4. Ubah perintah onpressed di productentry_form.dart menjasi seperti ini
```
onPressed: () async 
  if (_formKey.currentState!.validate()) {
      // Send to Django and wait for response
      final response = await request.postJson(
          "http://127.0.0.1:8000/create-flutter/",
          jsonEncode(<String, dynamic>{
              'productName': _product,
              'price': _price,  // Send as integer
              'description': _description,
              'rating': _rating,  // Send as integer
          }),
      );
      if (context.mounted) {
          // Now handle the response directly as a Map
          if (response['status'] == 'success') {
              ScaffoldMessenger.of(context)
                  .showSnackBar(const SnackBar(
              content: Text("Product successfully saved!"),
              ));
              Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(builder: (context) => MyHomePage()),
              );
          } else {
              ScaffoldMessenger.of(context)
                  .showSnackBar(const SnackBar(
                  content:
                      Text("An error occurred. Please try again."),
              ));
          }
      }
  }
```

* ### Step 7 : Implementasi Fitur Logout
1. Buatlah sebuah metode view untuk logout pada authentication/views.py
```
@csrf_exempt
def logout(request):
    username = request.user.username

    try:
        auth_logout(request)
        return JsonResponse({
            "username": username,
            "status": True,
            "message": "Logout berhasil!"
        }, status=200)
    except:
        return JsonResponse({
        "status": False,
        "message": "Logout gagal."
        }, status=401)
```
2. Jangan lupa untuk sambungkan url nya
3. Tambahkan code ini di product_card
```
else if (item.name == "Logout") {
    final response = await request.logout(
        // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
        "http://[APP_URL_KAMU]/auth/logout/");
    String message = response["message"];
    if (context.mounted) {
        if (response['status']) {
            String uname = response["username"];
            ScaffoldMessenger.of(context).showSnackBar(SnackBar(
                content: Text("$message Sampai jumpa, $uname."),
            ));
            Navigator.pushReplacement(
                context,
                MaterialPageRoute(builder: (context) => const LoginPage()),
            );
        } else {
            ScaffoldMessenger.of(context).showSnackBar(
                SnackBar(
                    content: Text(message),
                ),
            );
        }
    }
}
```
