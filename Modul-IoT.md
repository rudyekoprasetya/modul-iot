# Modul Praktikum Dasar Internet of Things
---

Penyusun **Rudy Eko Prasetya, S.Kom** - Blog [https://rudyekoprasetya.wordpress.com](https://rudyekoprasetya.wordpress.com/about)

![Pengenalan IoT](https://upload.wikimedia.org/wikipedia/commons/thumb/a/ab/Internet_of_Things.jpg/1200px-Internet_of_Things.jpg)

Modul ini disusun sebagai bahan ajar praktikum Internet of Things(IoT) Dasar untuk siswa atau Mahasiswa. Modul ini dibuat berdasarkan dokumentasi resmi dari Website Official Arduino yang dipersingkat agar mudah untuk dipraktekkan dan dipahami. Sehingga jika menginginkan panduan lengkap bisa merujuk ke [https://www.arduino.cc/](https://www.arduino.cc/).

Modul ini menggunakan lisensi [Creative Common](https://creativecommons.org/licenses/by-sa/4.0/) dengan atribut NonKomersial-BerbagiRupa dimana Lisensi ini mengizinkan setiap orang untuk menggubah, memperbaiki, dan membuat ciptaan turunan bukan untuk kepentingan komersial, selama mereka mencantumkan kredit dan melisensikan ciptaan turunan dengan syarat yang serupa dengan ciptaan asli.

Modul ini dibuat dengan menggunakan [Markdown](https://www.markdownguide.org/) dan akan terus di update seiring dengan pengalaman belajar dan mengajar penyusun. History perubahan atau pull request bisa diakses pada [https://github.com/rudyekoprasetya/LearningArduino](https://github.com/rudyekoprasetya/LearningArduino)

## Daftar Isi
---

- [Pengantar Teknologi IoT](#pengantar-teknologi-iot)
- [Mengenal Mikrokontroller NodeMCU](#mengenal-mikrokontroller-nodemcu)
- [Persiapan dan Installasi](#persiapan-dan-installasi)
- [Membuat LED Blynking](#membuat-led-blynking)
- [Penanganan Digital Input](#penanganan-digital-input)
- [Penanganan Analog Input](#penanganan-analog-input)
- [Koneksi dengan WiFi](#koneksi-dengan-wifi)
- [Penggunaan IoT Platform](#penggunaan-iot-platform)
- [Referensi](#referensi)
- [Tentang](#tentang)



## Pengantar Teknologi IoT
---

IoT (Internet Of Things) Merupakan suatu teknologi yang memungkinkan benda-benda disekitar kita terhubung dengan internet. Teknologi ini digagas oleh Kevin Ashton pada tahun 1999 dan mulai terkenal melalui Auto-ID Center di MIT. 

Pada Bulan Juni 2009 Asthon Berkomentar

> Internet of Things memiliki potensi untuk mengubah dunia seperti pernah dilakukan oleh Internet, bahkan mungkin lebih baik. (Ashton,2009) Penelitian pada Internet of Things masih dalam tahap perkembangan. Oleh karena itu, tidak ada definisi standar dari Internet of Things.

Teknologi yang paling sederhana adalah [GPS (Global Positioning System)](https://id.wikipedia.org/wiki/Sistem_Pemosisi_Global) yang sering kita gunakan dalam perangkat smartphone kita. Namun saat ini Teknologi ini banyak digunakan untuk proyek-proyek Smart City diberbagai wilayah di indonesia. Dimana pengunaan sensor-sensor yang terhubung dengan perangkat mikrokontroller akan memproses data dan mengirimkannya secara realtime ke suatu Server. Merujuk [Kesini](https://youtu.be/n-f8B76Hozk) untuk Penjelasan lebih lanjut.

IoT pada dasarnya tersusun atas beberapa komponen utama

![IoT Component](https://miro.medium.com/max/762/1*MKcZzx06YQB8ks7C5-4_Mg.jpeg)


- **Device/Sensor** Bagian ini merupakan komponen yang berfungsi untuk mengambil atau mengkoleksi data dari berbagai macam perangkat dan mengirimkan ke bagian atau komponen lainnya. Contohnya adalah, lampu, sensor cahaya, Sensor Suhu dan sensor-sensor lainnya serta mikrokontroller.
- **Connectivity** Bagian ini bertugas untuk mengkoneksikan atau mengirimkan data dari device ke platform atau komponen lainnya. Contohnya adalah WiFi, LAN, Bluetooth, dll
- **Data Processing** Pada komponen ini data akan disimpan dan diolah untuk mengetahui pola data. Contohnya adalah IoT Server, IoT Platform seperti [Blynk](https://blynk.io/), [Thingspeak](https://thingspeak.com/) dll 
- **User Interface** pada bagian ini data yang diolah dari Server akan ditampilkan kepada end user, biasanya dalam bentuk aplikasi web atau mobile.


Dalam IoT tidak lepas dari mikrokontroller. **Mikrokontroller** adalah sistem mikroprosesor lengkap yang terkandung di dalam sebuah chip. Mikrokontroler berbeda dari mikroprosesor yang digunakan dalam sebuah PC, karena di dalam sebuah mikrokontroler umumnya juga telah berisi komponen pendukung sistem minimal mikroprosesor, yakni memori dan antarmuka I/O, sedangkan di dalam mikroprosesor umumnya hanya berisi CPU saja.

Salah satu perangkat yang paling sederhana untuk memulai belajar pemrograman IoT adalah Arduino dimana alat ini menggunakan mikrokontroler ATMega. Sifat Arduino yang Open Source, membuat Arduino berkembang sangat cepat. Sehingga banyak lahir perangkat-perangkat sejenis Arduino. Seperti NodeMCU, ESP32, DFRDuino dan sebagainya.

![arduino](https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Arduino_Uno_-_R3.jpg/220px-Arduino_Uno_-_R3.jpg)

Banyak yang bertanya Arduino ini sebenarnya menggunakan bahasa pemprograman apa? Arduino sebenarnya menggunakan bahasa C, yang sudah disederhanakan. Sehingga orang awam pun bisa menjadi seniman digital, bisa mempelajari Arduino dengan mudahnya.

## Mengenal Mikrokontroller NodeMCU
---

Seperti yang sudah dijelaskan bahwa IoT membutuhkan suatu device mikrokontroller untuk mengelola data dari sensor atau ke sensor. Sala satunya adalah adalah NodeMCU.

**NodeMCU** adalah sebuah platform IoT yang bersifat opensource. Terdiri dari perangkat keras berupa System On Chip ESP8266 dari ESP8266 buatan [Espressif System](https://www.espressif.com/). 

NodeMCU dilengkapi modul ESP-12E yang beroperasi pada frekuensi 80-160MHz dilengkapi dengan 12bkB RAM dan 4MB Flash Memory yang digunakan untuk memprogram dan menyimpan data. NodeMCU dilengkap dengan tombol reset (RST) dan FLASH untuk meng upgrade firmware.

ESP8266 ini terintegrasi dengan 802.11 b/g/n WiFi, sehingga dapat tersambung dengan jaringan wireless dan berinteraksi dengan internet. ESP8266 memiliki tegangan operasional anatar 3 s/d 3,6 Volt dimana sumber power dari mikrokontroller ini adalah port micro USB.

NodeMCU memiliki total 30 PIN yang dapat digunakan dalam membangung suatu project IoT. Koneksi setiap pin bisa dilihat pada gambar dibawah ini

![pin NodeMCU](https://i2.wp.com/randomnerdtutorials.com/wp-content/uploads/2019/05/ESP8266-NodeMCU-kit-12-E-pinout-gpio-pin.png)

- **Power PIN** digunakan untuk power supply bagi sensor atau perangkat yang terhubung dengan NodeMCU.Tegangan yang dihasilkan adalah 3.3 Volt
- **GND PIN** digunakan untuk ground pada NodeMCU
- **GPIO PIN** NodeMCU memiliki beberapa PIN GPIO yang digunakan untuk kontrol LED, Tombol atau lainnya Disini pin yang sering digunakan adalah D0 sd D8 untuk sensor bertipe data digital.
- **I2C PIN** digunakan untuk menghubungkan dengan sensor yang membutuhkan koneksi I2C (Inter Integrated Circuit)
- **UART PIN** pin ini digunakan untuk kominikasi dengan modul seperti bluetooth yang membutuhkan Komunikasi fluid control. Pin yang digunakan adalah RX dan TX
- **Control PIN** digunakan untuk mengontrol chip, yaitu PIN EN digunakan untuk enable atau disable chip dan pin RST untuk reset chip serta WAKE pin untuk membangunkan pin saat mode deep sleep.
- **Analog PIN** dalam NodeMCU terdapat 1 pin Analog yang digunakan untuk periperal atau sensor yang bertipe data analog.
- **SDIO PIN** atau Secure Digital Input/Output Interface digunakan untuk komunikasi dengan dengan SD Card.
- **Tombol Reset dan Flash** digunakan untuk reset code atau flash rom dari chip.


## Persiapan dan Installasi
---

Dalam Modul ini karena kita akan menggunakan Mikrokontroller NodeMCU Untuk itu membutuhkan driver dan software pendukung seperti :

1. Arduino IDE bisa didownload [disini](https://www.arduino.cc/en/Main/Software_)
2. Driver NodeMCU CH340 [disini](https://sparks.gogo.co.nz/ch340.html)

Silahkan download dan install software diatas.

### Install driver CH340
1. Setelah Mendowload driver CH340 silahkan extract dan jalankan file **setup.exe**

![install diver ch40](https://2.bp.blogspot.com/-QyVEUUba9PM/Wd83wY73GqI/AAAAAAAADWA/QDWkg1SaAe8CJpGyoJXk9jJGShcQSKKIwCK4BGAYYCw/s1600/path_ch340g_setup.jpg)

2. Selanjutnya langsung klik install
![install driver](https://2.bp.blogspot.com/-TtCCSUHce7g/Wd84GGO8RoI/AAAAAAAADWM/gLRFWKuJWOgP8xUfuqe5d_NVRbUwkYDwwCK4BGAYYCw/s1600/ch340g_install_window.jpg)

3. Koneksikan NodeMCU dengan komputer atau laptop anda via kabel USB. Kemudian buka **Device Manager** dan pastikan pada bagian **Port(COM&LPT)** sudah terinstall diver CH340
![device manager](https://3.bp.blogspot.com/-3n5Kk7N1o8c/Wd84ULu9aJI/AAAAAAAADWU/qynH3m2ju04iVUYR2h8IW9OHYeA8-RJEwCK4BGAYYCw/s1600/ch340g_installed_successfully.jpg)

**Amati dan perhatikan nilai COM pada device manager tersebut, dicontoh adalah COM19 hal ini biasanya berbeda pada setiap komputer atau laptop**

### Install Board ESP8266 di Arduino IDE
1. Pastikan komputer atau laptop terhubung dengan internet kemudian buka Aplikasi Arduino IDE yang sudah di install sebelumnya

2. Setelah aplikasi terbuka, pilih menu **File > Preference** , perhatikan gambar di bawah ini
![install esp8266 1](https://4.bp.blogspot.com/-snqERb01FV0/XG_Yt_cdsCI/AAAAAAAAAU8/KESbVYwbsEwiutTdfcBlbF4iJVOGC4OJwCLcBGAs/s1600/Screenshot_132.png)

3. Apabila Preference telah di klik maka akam muncul sebuah pop up jendela baru seperti gambar dibawah ini.
![install esp8266 2](https://1.bp.blogspot.com/-3596kGOdQGM/XG_ZCvEL0BI/AAAAAAAAAVE/GOxfR-kIluoRRxXeEqk4bjodT42OQny-ACLcBGAs/s1600/Screenshot_133.png)

4.  Perhatikan tanda panah berwarna merah, klik pada bagian tersebut, lalu akan muncul jendela pop up baru lagi, perhatikan gambar di bawah ini.
![install esp8266 2](https://2.bp.blogspot.com/-tQrP9qd4fxE/XG_ZZqHEfsI/AAAAAAAAAVM/rxd_Fn9ix7AQ1fmzd--eYW2D5hO7zmZ9gCLcBGAs/s1600/Screenshot_134.png)

5. Masukan code berikut ini kemudian klik OK
```console
http://arduino.esp8266.com/stable/package_esp8266com_index.json
```

6. Kemudian pergi ke menu **Tools >  Board > Boards Manager** , perhatikan gambar di bawah ini.
![install esp8266 3](https://2.bp.blogspot.com/-4xgK8NS5gZc/XG_aPCt1NRI/AAAAAAAAAVY/S_ydkjYniVUro4-ULreYD8usosE86Ax9QCLcBGAs/s1600/Screenshot_135.png)

7. Setelah membuka **Boards Manager** langkah selanjutnya adalah mengetikkan nama **ESP8266** di kolom pencarian, kemudian klik Install, karena pada tutorial ini saya sudah menginstall board ESP8266 maka tombol tersebut berganti menjadi update, jika temen-temen belum pernah menginstall board ESP8266 maka tombol tersebut bertuliskan **Install** 
![install esp8266 4](https://4.bp.blogspot.com/-Z5ssIf6FJyM/XG_qaqZSY8I/AAAAAAAAAVk/P3dSJjwF06MrLFgYMssY3UcdG9_sTinJwCLcBGAs/s1600/Screenshot_136.png)

8. Tunggu sampai proses selesai, Untuk cek hasil install silahkan pergi ke menu **Tools > Board** pastikan ada Board NodeMCU seperti dibawah ini
 ![install esp8266 5](https://4.bp.blogspot.com/-KUf2PHOJOtM/XNZfT6SINzI/AAAAAAAAGLo/2Dqz_GO2LWQsNNoELoCdG5O7CovfURKDwCK4BGAYYCw/s640/9.%2BPilih%2Bboard.jpg)

 Sampai sini kita sudah siap untuk membuat aplikasi IoT.


## Membuat LED Blynking
---

Kali ini kita akan membuat project sederhana yaitu led yang berkedip, sebelum itu kita harus mengenal karakteristik dan komponen elektronika seperti LED, Breadboard dan Resistor. 

**LED (Light Emitting Diode)** adalah suatu semikonduktor yang memancarkan cahaya monokromatik yang tidak koheren ketika diberi tegangan. Warna-warna Cahaya yang dipancarkan oleh LED tergantung pada jenis bahan semikonduktor yang dipergunakannya.

![LED](https://1.bp.blogspot.com/-mXtq1YSdco4/X3g5Ie2uuFI/AAAAAAAABHY/SiLLoWDsPW0xWE2Edco-D8-lnYliU2_HACLcBGAsYHQ/s1600/Karakteristik%2BLED.png)

Untuk mengetahui polaritas terminal Anoda (+) dan Katoda (-) pada LED. Kita dapat melihatnya secara fisik berdasarkan gambar diatas. Ciri-ciri Terminal Anoda pada LED adalah kaki yang lebih panjang dan juga Lead Frame yang lebih kecil. Sedangkan ciri-ciri Terminal Katoda adalah Kaki yang lebih pendek dengan Lead Frame yang besar serta terletak di sisi yang Flat.

**Breadboard** adalah papan yang digunakan untuk membuat rangkaian elektronik sementara dengan tujuan uji coba atau prototipe tanpa harus menyolder. Dengan memanfaatkan breadboard, komponen-komponen elektronik yang dipakai tidak akan rusak dan dapat digunakan kembali untuk membuat rangkaian yang lain. Breadboard umumnya terbuat dari plastik dengan banyak lubang-lubang diatasnya. Lubang-lubang pada breadboard diatur sedemikian rupa membentuk pola sesuai dengan pola jaringan koneksi di dalamnya.

![breadboard](http://blog.famosastudio.com/wp-content/uploads/2011/06/MediumBreadboard-ConnectionLayout.jpg)

Gambar diatas adalah medium breadboard dengan 400 titik koneksi. Medium breadboard ini biasa juga disebut half (setengah) breadboard. Pada breadboard tersebut dapat dilihat penulisan huruf A, B, C, D, E, F, G, H, I dan J. Kemudian ada angka 1, 5, 10, 15 dan 20. Huruf dan angka ini membentuk semacam koordinat. A1, B1, C1, D1 dan E1 saling berhubungan sesuai pola koneksinya (lihat kembali garis berwarna biru). Begitu juga A2 –> E2, A3 –> E3, F1 –> J1, F2 –> J2 dan seterusnya. Dengan memahami pola koneksi ini kita sudah bisa memakai breadboard untuk keperluan prototipe rangkaian sehingga dapat menempatkan komponen elektronik secara tepat sesuai gambar rangkaian yang dimaksud.

**Resistor** merupakan komponen elektronik yang memiliki dua pin dan didesain untuk mengatur tegangan listrik dan arus listrik. Resistor mempunyai nilai resistansi (tahanan) tertentu yang dapat memproduksi tegangan listrik di antara kedua pin. Satuan untuk resistansi listrik adalah Ohm.

![resistor](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e3/3_Resistors.jpg/338px-3_Resistors.jpg)


Setelah memahami beberapa komponen dasar kita bisa praktikum dan siapkan komponen-komponen berikut ini
1. NodeMCU 1x
2. Breadboard 1x
3. LED 1x
4. Resistor 1K Ohm 1x
5. Kabel Jumber 1x

Kemudian rangkailah seperti gambar dibawah ini
![Rangkaian Led](https://i.ibb.co/9Yq8SJz/iot1.jpg)

Dalam rangkaian tersebut kita hubungkan PIN D5 dengan Anoda(+) dari led sedangkan untuk pin GND dihubungkan dengan Katoda(-) namun sebelumnya kita berikan resistor agar led tidak kelebihan muatan.

Bukalah Arduino IDE Anda dan ketikan code dibawah ini

```c++
int ledMerah = D5 //untuk definisi PIN yang digunakan LED Merah

void setup() {
    pinMode(ledMerah, OUTPUT); 
}

void loop() {
    digitalWrite(ledMerah, HIGH); //menyala
    delay(1000); //jeda 1 detik atau 1000 milisecond
    digitalWrite(ledMerah, LOW); //mati
    delay(1000);
}
```
Simpan code diatas dengan nama file **belajar_led.ino** kemudian Hubungkan NodeMCU dengan komputer atau laptop via USB, Kemudian klik Menu **Tools > Board > pilih NodeMCU 1.0**

Kemudian pastikan pula di Menu **Tools > Ports > COM19 [sesuiaikan]** sesuai dengan COM Port dari Driver NodeMCU yang ada pada device manager yang sudah dijelaskan sebelumnya.

Untuk cek tekan **tombol Cek pada pojok Kanan Atas**, jika tidak ada pesan error anda bisa langsung upload dengan klik **tombol Panah Kanan** di sebelahnya.

![upload and verify](https://i.ibb.co/99kxTGz/arduino-ide.jpg)

Tunggu sampai proses upload code selesai dan Amatilah LED Anda. 

Coding `digitalWrite()` digunakan untuk mengirim data digital ke PIN untuk mengontrol LED baik HIGH yang berarti menyala atau LOW berati mati.

Selanjutnya ubah codenya menjadi dibawah ini

```c++
int ledMerah = D5; //untuk definisi PIN yang digunakan LED Merah

void setup() {
    pinMode(ledMerah, OUTPUT); 
}

void loop() {
    analogWrite(ledMerah, 100); //menyala
    delay(1000); //jeda 1 detik
    analogWrite(ledMerah, 25); //mati
    delay(1000);
}
```
Coba upload kembali code diatas ke NodeMCU anda dan amatilah hasilnya

Fungsi code `analogWrite()` adalah untuk menyalakan LED dengan nilai kecerahan yang bisa diatur. Rentan nilai yang bisa dimasukan biasanya antara 0 s/d 255. 

### latihan
1. Buat rangkain dengan 3 LED semisal Led Merah, Kuning, Hijau dimana led tersebut menyala bergantian
2. Masih dengan rangkaian yang sama buatlah led tersebut menyala bergantian dengan ketentuan
    - led merah menyala selama 3 detik
    - led kuning menyala selama 2 detik
    - led hijau menyala selama 1 detik


## Penanganan Digital Input
---

Pada Bab sebelumnya kita belajar mengenai digital output untuk menyalakan atau mematikan LED. Kali ini kita akan belajar bagaimana cara mengelola digital input pada proyek IoT kita.

Untuk praktikum siapkan komponen berikut ini
1. NodeMCU 1x
2. Breadboard 1x
3. LED 1x
4. Resistor 1K Ohm 2x
5. Push Button 1x
6. Kabel Jumper

Selanjutnya rangkai seperti gambar dibawah ini

![rangkaian 2](https://i.ibb.co/P5ZnJ5K/iot2.jpg)

dalam Rangkaian tersebut PIN yang digunakan adalah PIN D7 untuk LED Hijau kemudian PIN D8 untuk PushButton dan PIN 3.3 V untuk arus ke Push button beserta PIN GND untuk groundnya.

Selanjutnya buka Arduino IDE buat file baru dan ketikan kode dibawah ini

```c++
int ledHijau = D5; 
int tombol = D6;

void setup(){
    //mode pin untuk mengeluarkan tegangan / output
    pinMode(ledHijau, OUTPUT);
    //mode pin untuk membaca hasil / input
    pinMode(tombol, INPUT);
    //untuk mengkatifkan Komunikasi Serial
    Serial.begin(9600);
}

void loop() {
    //membaca nilai tombol dan menyimpan dalam variable
    int hasil_tombol = digitalRead(tombol);
    //menampikan hasil pada serial Monitor
    Serial.print("nilai tombol = ");
    Serial.println(hasil_tombol);
    delay(500);
}
```

Kita sudah mengetahui bahwa untuk pinMode dari LED adalah OUTPUT Namun beda dengan push button yaitu pinMode yang digunakan adalah INPUT. Untuk kode `Serial.begin(9600)` digunakan untuk mengaktifkan debugging yang nantinya kita gunakan serial monitor dari Arduino IDE. Kode `digitalRead(tombol)` berguna untuk membaca hasil tombol. Untuk kode `Serial.print()` digunakan untuk menampilkan tulisan atau karakter ke serial monitor.

Selanjutnya simpan code diatas dengan nama file **belajar_input.ino**. Jangan lupa Hubungkan NodeMCU dengan komputer atau laptop via USB

Hubungkan NodeMCU dengan komputer atau laptop via USB Untuk verifikasi code. Selanjutnya tekan **tombol Cek**, jika tidak ada pesan error anda bisa langsung upload dengan klik **tombol Panah Kanan** di sebelahnya.

Coba buka menu **Tools > Serial Monitor** atau bisa tekan tombol keyboard **CTRL + SHIFT + M**.

Cobalah tekan tombol dan lepas tombol dan amatilah hasil yang ditampilkan pada serial monitor.

Disini kita bisa amati bahwa bila tombol ditekan akan mengirimkan nilai 1 sedangkan bila dilepas akan mengirimkan hasil 0.

Ubahlah kode menjadi dibawah ini

```c++
int ledHijau = D5; 
int tombol = D6;

void setup(){
    //mode pin untuk mengeluarkan tegangan / output
    pinMode(ledHijau, OUTPUT);
    //mode pin untuk membaca hasil / input
    pinMode(tombol, INPUT);
    //untuk mengkatifkan Komunikasi Serial
    Serial.begin(9600);
}

void loop() {
    //membaca nilai tombol dan menyimpan dalam variable
    int hasil_tombol = digitalRead(tombol);
    //menampikan hasil pada serial Monitor
    Serial.print("nilai tombol = ");
    Serial.println(hasil_tombol);
    delay(500);
    //jika tombol ditekan
    if(hasil_tombol == 1) {
        digitalWrite(ledHijau, HIGH); //led menyala
    } else {
        digitalWrite(ledHijau, LOW); //lampu mati
    }
}
```

Coba upload kembali ke NodeMCU Anda kemudian tekan push buttonnya. *Apakah yang terjadi??*

Selain menangani digital input dari saklar atau push button, kita jua bisa mengelola input dari keyboard komputer atau laptop yang tersambung dengan NodeMCU.

Coba buat rangkaian sederhana 1 LED seperti bab sebelumnya.
![Rangkaian Led](https://i.ibb.co/9Yq8SJz/iot1.jpg)

Kemudian ketikan kode dibawah ini

```c++
int ledMerah = D5; //untuk definisi PIN yang digunakan LED Merah

void setup() {
    pinMode(ledMerah, OUTPUT); 
    //untuk serial
    Serial.begin(9600);
}

void loop() {
    if(Serial.available() > 0) {
        //membaca tombol keyboard yang ditekan
        int nilai_keyboard = Serial.read();

        //menampilkan ke serial monitor
        Serial.print("tombol keyboard = ");
        Serial.println(nilai_keyboard);
        delay(500);

        //jika ditekan tombol 1
        if(nilai_keyboard == '1') {
            //nyalakan led
            digitalWrite(ledMerah, HIGH);
        } else if(nilai_keyboard == '2') {
            //matikan led
            digitalWrite(ledMerah, LOW);
        }
    }
```

Untuk nomor pin disini menggunkan pin D5 untuk led Merah.  Kode `if(Serial.available() > 0)` digunakan untuk cek apakah ada komunikasi serial atau tombol keyboard yang ditekan. Kode `int nilai_keyboard = Serial.read();` digunakan untuk menampung input user saat menekan tombol keyboard dan disimpan dalam variabel *nilai_keyboard*. Tiap input keyboard yang dibaca akan dibandingkan dengan struktur percabangan if untuk control LED.

Simpan kode diatas dengan nama **belajar_kontrol.ino** selanjutnya lakukan verifikasi code diatas sebelum upload. Jika sudah di upload coba buka serila Monitor, ketikan angka 1 kemudian tekan enter. Amatilah hasilnya.

### latihan
1. Rangkailah 3 Led dengan warna bebas (misal led1, led2, led3) beserta 1 push button. Aturlah agar bila ditekan push button maka 3 led tadi akan menyala secara bergantian dengan jeda 1 detik.
2. Ubah aplikasi IoT diatas dengan menambahkan kontrol Keyboard laptop atau komputer dengan ketentuan
    - Bila ditekan tombol keyboard **1** maka led1 lama menyala 3 detik
    - Bila ditekan tombol keyboard **2** maka led2 lama menyala 2 detik
    - Bila ditekan tombol keyboard **3** maka led3 lama menyala 3 detik
    - Bila ditekan tombol keyboard **4** maka semua led menyala
    - Bila ditekan tombol keyboard **5** maka semua led mati


## Penanganan Analog Input
---

Kali ini kita akan belajar menggunaan sensor cahaya atau **LDR (Light Dependent Resistor)**. LDR memiliki nilai hambatan 200 Kilo Ohm pada saat dalam kondisi sedikit cahaya (gelap), dan akan menurun menjadi 500 Ohm pada kondisi terkena banyak cahaya.

![LDR](https://5.imimg.com/data5/LF/JE/MY-21614932/ldr-light-dependent-resistor-500x500.jpg)


Baik langsung saja kita lakukan praktikum. Kita akan membuat lampu LED yang akan menyala otomatis saat gelap dan mati saat kondisi terang. Siapkan komponen dibawah ini

- NodeMCU 1x
- Resistor 1K Ohm 2x 
- LED 1x
- Breadboard 1x
- LDR 1x
- Kabel Jumper

Rangkailah seperti gambar dibawah ini
![Rangkaian LDR](https://i.ibb.co/ySc53YZ/iot3.jpg)

Pada rangkaian diatas sensor LDR mendapatkan tegangan dari pin 3.3 V dan GND kemudian diberikan resistor di jalur GND. Pin Analog A0 di letakknya salah satu pin sensor yang akan digunakan untuk membaca hasil sensor. Kemudian di pasang LED di PIN D1.

Untuk codenya adalah sebagai berikut ini

```c++
//inisialisasi pin led dan sensor
int led = D1; //untuk led
int sensor = A0; //untuk sensor cahaya
int hasil; //untuk hasil dari bacaan sensor

void setup() {
    pinMode(led, OUTPUT); //untuk setting PIN LED
    pinMode(sensor, INPUT); //untuk membaca hasil sensor
    Serial.begin(9600);
}
void loop() {
    //menampung hasil sensor ke variabel
    hasil = analogRead(sensor);
    //menampilkan hasil sensor ke serial monitor
    Serial.print("Hasil dari sensor adalah ");
    Serial.println(hasil); 

    if(hasil<10) {
        digitalWrite(led,HIGH); //jika gelap maka lampu menyala
    } else {
        digitalWrite(led,LOW); //jika terang maka lampu mati
    }

    delay(500);
}
```  

Untuk konfigurasi pada kode `pinMode(led, OUTPUT);` digunakan untuk konfigurasi LED di pin D2 sedangkan kode `pinMode(sensor, INPUT);` untuk konfigurasi pin A0. Kode `hasil = analogRead(sensor);` digunakan untuk menampung nilai hasil pembacaan sensor kedalam variabel hasil.

Pada struktur percabangan kode `if(hasil<10)` adalah untuk kondisi dimana LED akan menyala atau mati. Silahkan diatur sesuai dengan keinginan dan
itensitas cahaya yang diinginkan. angka 10 diperoleh dari pembacaan nilai dari sensor dimana ada jumlah arus listrik yang dibaca sensor, jika cahaya kurang maka nilai akan rendah sebaliknya jika cahaya intensitas tinggi maka nilai akan naik. Kode nya adalah `Serial.print("Hasil dari sensor adalah "); Serial.println(hasil);`

Simpan kode diatas dengan nama **belajar_sensor.ino** Untuk menguji hasil silahkan upload kode diatas dan buka serial monitor. Cobalah untuk menutup sensor agar intensitas cahaya berkurang dan amatilah hasilnya.

### latihan
1. Buatlah Rangkaian IoT untuk prototipe smart traffic light dengan ketentuan
    - Terdapat 3 LED (misal merah, kuning, hijau)
    - Jika kondisi siang / banyak cahaya maka Led akan menyala bergantian dengan ketentuan
        - LED merah menyala selama 3 detik
        - Kemudian LED kuning menyala selama 1 detik
        - Dilanjutkan LED hijau menyala selama 2 detik
    - Jika kondisi malam / sedikit cahaya maka yang menyala hanya LED kuning secara berkedip kedip


## Koneksi Dengan WiFi
---

Seperti yang sudah kita ketahui bahwa NodeMCU berbasiskan Chip ESP8266 dimana sudah ada modul WiFi didalamnya. Sehingga kita bisa menghubungkanya dengan jaringan seperti jaringan internet.

Untuk praktikum bukalah Arduino IDE anda dan buat file baru, ketikan code dibawah ini

```c++
#include <ESP8266WiFi.h> //import library Wifi ESP8266

const char *ssid = "coba"; //ganti nama hotspot
const char *pass = "rahasia";//ganti password

//inisialisasi Wifi Client
WiFiClient client;

void setup() {

    //aktifkan serial komunikasi
    Serial.begin(9600);
    delay(10);

    Serial.print("Connect to :");
    Serial.println(ssid);

    //memulai koneksi ke ssid dan password hotspot
    WiFi.begin(ssid, pass);

    //jika belum terkoneksi munculkan titik-titik ......
    while (WiFi.status() != WL_CONNECTED) {
      delay(500);
      Serial.print("...");
    }

    //jika terkoneksi munculkan IP Address beserta nama hotspot
    Serial.print("\n");
    Serial.print("IP address : ");
    Serial.print(WiFi.localIP());
    Serial.print("\n");
    Serial.print("Connect to : ");
    Serial.println(ssid);
}
void loop() { 

}
```

Simpan dengan nama **belajar_wifi.ino** kemudian upload ke NodeMCU anda. Kemudian coba buka serial Monitor dan amatilah apa yang muncul.

![NodeMCU WiFi](https://miro.medium.com/max/700/1*DRfjf0kPandO0aERHdB9zg.png)


saat status wifi tidak tersambung maka akan melakukan perulangan mencetak string “…” 

Jika berhasil maka pada serial monitor akan muncul IP address yang terkoneksi pada SSID. Seperti yang diatas, nodemcu mempunyai IP address 192.168.43.114.

Jika ingin menampilkan Mac Address dari NodeMCU cukup ditambahkan kode dibawah ini.

```c++
Serial.print("\n");
Serial.print("MAC : ");
Serial.print(WiFi.macAddress());
```

Maka hasilnya adalah sebagai berikut ini

![Wifi Mac Address](https://miro.medium.com/max/700/1*iIV9wCu3zPmxdfNwvfaR1A.png)

Jika anda ingin mengkoneksikan ulang Cukup ditekan tombol **RST** pada NodeMCU maka secara otomatis akan mencari koneksi ke hotspot yang sudah di daftarkan.

Selanjutnya kita akan mencoba praktikum mengontrol LED dengan web server bawaan NodeMCU. 

Silahkan buat rangkaian sederhana 1 LED seperti dibawah ini

![Rangkaian Led](https://i.ibb.co/9Yq8SJz/iot1.jpg)

Kemudian ketikan kode dibawah ini

```c++
#include <ESP8266WiFi.h> //import library Wifi ESP8266
#include <ESP8266WebServer.h> //import library web Server

const char *ssid = "coba"; //ganti nama hotspot
const char *pass = "rahasia";//ganti password

int ledMerah = D5 //untuk definisi PIN yang digunakan LED Merah

//inisialisasi Wifi Client
WiFiClient client;

//inisialisasi Web Server pada port 80
ESP8266WebServer server(80);


void setup() {
    //pin Mode Led Merah
    pinMode(ledMerah, OUTPUT);

    //aktifkan serial komunikasi
    Serial.begin(9600);
    delay(10);

    Serial.print("Connect to :");
    Serial.println(ssid);

    //memulai koneksi ke ssid dan password hotspot
    WiFi.begin(ssid, pass);

    //jika belum terkoneksi munculkan titik-titik ......
    while (WiFi.status() != WL_CONNECTED) {
      delay(500);
      Serial.print("...");
    }

    //jika terkoneksi munculkan IP Address beserta nama hotspot
    Serial.print("\n");
    Serial.print("IP address : ");
    Serial.print(WiFi.localIP());
    Serial.print("\n");
    Serial.print("Connect to : ");
    Serial.println(ssid);

    //membuat tampilan web utama saat diakses http://ip_address
    server.on("/", [](){
        server.send(200, "text/html", "<b>Welcome To NodeMCU WebServer</b>");
    });

    //perintah url untuk menyalakan lampu http://ip_address/ledon
    server.on("/ledon", [](){
        server.send(200, "text/html", "<b>Led Menyala</b>");
        //nyalakan LED
        digitalWrite(ledMerah, HIGH);
    });

    //perintah url untuk mematikan lampu http://ip_address/ledoff
    server.on("/ledoff", [](){
        server.send(200, "text/html", "<b>Led Mati</b>");
        //mematikan LED
        digitalWrite(ledMerah, LOW);
    });

    //mulai menjalankan web server
    server.begin();
}
void loop() { 
    //membaca request dari client
    server.handleClient();
}
```

Simpan dengan nama **belajar_webserver.ino** lalukan verifikasi kode kemudian upload ke nodemcu anda.

buka serial monitor pastikan NodeMCU sudah mendapatkan IP Address seperti dibawah ini

![NodeMCU WiFi](https://miro.medium.com/max/700/1*DRfjf0kPandO0aERHdB9zg.png)

Coba bukalah web browser (Chrome, Mozilla dll) pada laptop anda, namun koneksikan terlebih dahulu dengan hotspot yang sama dengan NodeMCU anda. Kemudian ketikan url IP Address dari NodeMCU seperti  `http://192.168.43.114` *Tulisan apakah yang muncul?*

Selanjutnya cobalah buka url `http://192.168.43.114/ledon` amatilah hasilnya. Begitu pula buka url `http://192.168.43.114/ledoff`,*Apakah yang terjadi dengan rangkaian LED kita?*

NodeMCU bisa dijadikan sebuah web server dengan mengaktifkan library `#include <ESP8266WebServer.h>`. Dalam komunikasi via web server di port HTTP yaitu port 80 kita bisa memberikan respon sesuai dengan request dari client dengan Kode dibawah ini. 

```c++
server.on("/url_parameter", [](){
    server.send(200, "text/html", "kode HTML");
    //perintah lain yang dijalankan saat url diakses    
});
```

Sehingga kita bisa memberikan respon seperti text HTML saat url tersebut dibuka di browser client.

### latihan
1. Buatlah aplikasi Web IoT dengan Webserver NodeMCU dengan 3 Led dengan warna bebas (misal led1, led2, led3) Aturlah 3 led tadi akan menyala secara bergantian dengan ketentuan
    - Bila diakses url `http://ip_address/on1` maka **hanya led1 yang menyala** 
    - Bila diakses url `http://ip_address/on2` maka **hanya led2 yang menyala** 
    - Bila diakses url `http://ip_address/on3` maka **hanya led3 yang menyala** 
    - Bila diakses url `http://ip_address/onall` maka **semua led menyala** 
    - Bila diakses url `http://ip_address/offall` maka **semua led mati** 
2. Masih menggunakan Rangkaian 3 led diatas buatlah aplikasi Web IoT dengan Webserver NodeMCU dengan ketentuan
    - Bila diakses url `http://ip_address/blynk` maka **3 led akan nyala berkedip bergantian**
    - Bila diakses url `http://ip_address/off` maka **3 led akan mati semua**

## Penggunaan IoT Platform
---

**Platform IoT** adalah suatu ekosistem yang digabungkan untuk menjadi wadah pembuatan produk dan solusi IoT agar efisien dan tidak memakan banyak waktu.

![Ilustrasi platform](https://i1.wp.com/danielelizalde.com/wp-content/uploads/2016/11/IoT-Stack.png)

Platform IoT disini sebagai server atau cloud yang siap dipakai untuk suatu produk atau bisnis. Platform IoT dapat digunakan untuk mengumpulkan data dari berbagai sumber, menyimpan data, menampilkan data, mengontrol perangkat, mengelola inventory perangkat dan lain-lain.

Ada banyak sekali platform IoT yang bisa digunakan dari yang berbayar sampai yang free alias gratis. Untuk contoh platform yang gratis adalah

1. [Thingspeak](https://thingspeak.com)
2. [Blynk](https://blynk.io)
3. [Thingsboard](https://thingsboard.io)
4. [Firebase](https://firebase.google.com/?hl=id)

Pada modul kali ini saya akan menggunakan Firebase Realtime database untuk dijadikan sebagai IoT Platform praktikum kita. 

![firebase](https://upload.wikimedia.org/wikipedia/commons/thumb/b/bd/Firebase_Logo.png/375px-Firebase_Logo.png)

Menurut [Wikipedia](https://id.wikipedia.org/wiki/Firebase) **Firebase** adalah

> Suatu layanan dari Google yang digunakan untuk mempermudah para pengembang aplikasi dalam mengembangkan aplikasi. Dengan adanya Firebase, pengembang aplikasi bisa fokus mengembangkan aplikasi tanpa harus memberikan usaha yang besar.

Firebase akan digunakan untuk menyimpan data status LED dan hasil pembacaan Sensor LDR. Berikut adalah rangkaiannya

![Rangkaian LDR](https://i.ibb.co/ySc53YZ/iot3.jpg)


Untuk langkah pertama kita buat realtime database baru di firebase. Sebelum itu pastikan anda miliki akun google.

![firebase homepage](https://i.ibb.co/hfVQ6P1/firebase1.jpg)

Klik tombol mulai dan masukan akun google anda. Setelah itu klik **Add Project**

![Add project](https://i.ibb.co/gPXBC7t/firebase2.jpg)

Kemudian kita isikan nama project kita, semisal **belajar-nodemcu** seperti dibawah ini. Nama project disini harus unik, jika sudah ada maka kita harus memilih nama lainnya. Selanjutnya tekan tombol **Continue**

![new project](https://i.ibb.co/Qbqfh2Y/firebase3.jpg)


Selanjutnya pilih **continue** untuk melanjutkan 

![continue project](https://i.ibb.co/x7ShYdb/firebase4.jpg)

Kemudian arahkan akun analytic pada akun gmail anda, kemudian klik **Create Project**

![create project](https://i.ibb.co/y8Qyyv2/firebase5.jpg)

Tunggulah sampai proses pembuatan project selesai.

Jika sudah berhasil maka akan muncul tampilan dibawa ini

![firebase database](https://i.ibb.co/F7FKrpK/firebase6.jpg)

Untuk membuat database baru klik menu **Realtime Database** kemudian klik tombol **Create Database**

![Create database](https://i.ibb.co/b1WfJBW/firebase7.jpg)

Kemudian pada database option biarkan untuk Location United State, kemudian klik **Next**

![location database](https://i.ibb.co/JKfJZ5L/firebase8.jpg)

Kemudian kita diminta untuk menentukan _Security Rules_ untuk database kita. ada 2 pilihan yaitu

- **Locked Mode** : dimana secara default database kita itu private jadi tidak bisa di tulis atau dibaca oleh client. kita perlu mendefinikan rules atau aturan untuk akses database kita.
- **Test Mode** : Mode ini semua akses database kita terbuka, namun setiap 30 hari kita harus update security rules kembali

karena kita masih ujicoba kita pilih Test Mode, Klik **Enable** kemudian tunggu sampai proses pembuatan database selesai.

![security rules](https://i.ibb.co/z29pdf3/firebase9.jpg)

Ketika sudah selesai maka akan muncul seperti dibawah ini

![database firebase](https://i.ibb.co/N7ghb1F/firebase10.jpg)

yang perlu **dicatat dan diperhatikan** adalah nama host database. Seperti contoh diatas nama hostnya adalah **https://belajar-d9455-default-rtdb.firebaseio.com/**. 

Selain itu kita perlu mencatat pula untuk _secret key_ atau _token_ database kita. Klik tanda gear pada **Project Overview**

![token](https://i.ibb.co/G5GsHfz/firebase11.jpg)

Selanjutnya klik Tab **Service Accounts** kemudian Klik **Database Secret**. Klik **show** pada bagian titik-titik untuk melihat token atau secret jangan lupa copy ke notepad untuk menyimpannya.

![database secret](https://i.ibb.co/dBd4xD2/firebase12.jpg)

Untuk membuat data dalam hal ini dalam firebase di sebut _child_  klik tanda + pada nama database kita contoh `belajar-d9455-default-rtdb:` kemudian isikan **key** dan **value** nya, semisal kita buat key dengan nama **data** seperti dibawah ini

![database fb](https://i.ibb.co/602M9sH/database-fb1.jpg)

Kemudian kita buat child didalam data dengan klik tanda + untuk key dan value **ledStatus** dan **sensor** seperti dibawah ini

![database fb2](https://i.ibb.co/b17SYN5/database-fb2.jpg)

Dimana _ledStatus_ digunakan untuk menyimpan data led, disini saya isi angka 1 berarti led dalam status menyala. Sedangkan key _sensor_ untuk menyimpan data sensor, sebagai contoh sensor LDR. Klik tombol **Add** untuk menyimpannya.

Sampai disini kita sudah membuat platform atau tempat menyimpa data untuk project kita. Selanjutnya kita akan menginstall atau memasukan **library Arduino Firebase** untuk coding kita di Arduino IDE.

Pertama Download FirebaseArduino Library di [https://github.com/FirebaseExtended/firebase-arduino/archive/v0.3.zip](https://github.com/FirebaseExtended/firebase-arduino/archive/v0.3.zip)

Kemudian pada arduino IDE pilih **sketch > include library > Add .zip Library**

![add zip library](https://berqas.com/wp-content/uploads/2020/03/image-10.png)

Pilih file **firebase-arduino.zip** yang telah didownload

Selanjutnya kita butuh penyesuaian untuk FINGERPRINT silahkan buka url ini di browser 

```console
https://www.grc.com/fingerprints.htm?domain=host_firebase_anda
```

ganti host dengan host database anda misal dicontoh `https://www.grc.com/fingerprints.htm?domain=belajar-d9455-default-rtdb.firebaseio.com`

sehingga muncul website seperti dibawah ini

![fingerprint](https://i.ibb.co/BP1xfKm/fingerprint.png)

Copy kode hexa untuk fingerprint database kita. 

Kemudian silahkan buka file **FirebaseHttpClient.h** pada folder **libraries\firebase-arduino\src** dengan code editor atau notepad. Ganti fingerprintnya dengan fingerprint yang sudah kita dapatkan sebelumnya

```console
static const char kFirebaseFingerprint[] =
      "6E:F3:55:47:6D:F1:0E:5B:2B:04:F2:F8:C0:8B:E8:05:65:0F:1A:C1"; // 2020-02 paste dengan fingerprint yang baru
```

Jika sudah simpan dan tutup file tersebut.

Library Arduino Firebase membutuhkan library dependensi yaitu ArduinoJSON. untuk install Pastikan laptop atau komputer anda terhubung dengan internet kemudian buka menu **Sketch > Include Libraries > Manage libaries**. Selanjutnya ketikan di filter **Arduinojson**, Pilih **versi 5.13.x** kemudian Klik **install** pada library **ArduinoJson by Benoit Blachon** seperti dibawah ini.

![install arduinojson](https://i.ibb.co/Y297sCR/arduinojson.png)

Tunggu sampai proses installasi selesai.

Kemudian ketikan coding dibawah ini pada arduino IDE

```c++
//include library wifi 
#include <ESP8266WiFi.h>
//include library Firebase Arduino
#include <FirebaseArduino.h>

//isi dengan nama host nama database anda tanpa http:// dan tanda /
#define FIREBASE_HOST "contoh.firebaseio.com"
//isi dengan database secret database kita
#define FIREBASE_AUTH "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
//isi dengan konfigurasi wifi anda
#define WIFI_SSID "hotspot_anda"
#define WIFI_PASSWORD "password_hotspot"

//pin yang digunakan untuk led 
int led = D1;
//pin sensor LDR
int ldr = A0;

void setup() {
  //konfigurasi serial dan pin mode
  Serial.begin(9600);
  pinMode(led, OUTPUT);
  pinMode(ldr, INPUT);

  // connect to wifi.
  WiFi.begin(WIFI_SSID, WIFI_PASSWORD);
  Serial.print("connecting");
  while (WiFi.status() != WL_CONNECTED) {
    Serial.print(".");
    delay(500);
  }
  Serial.println();
  Serial.print("connected: ");
  Serial.println(WiFi.localIP());
  
  //memulai koneksi dengan firebase
  Firebase.begin(FIREBASE_HOST, FIREBASE_AUTH);

  //buat data di database
  //status led dan sensor defaultnya 0
  Firebase.setInt("data/ledStatus", 0);
  Firebase.setFloat("data/sensor", 0);
}

void loop() {
  //cek kondisi ledStatus di database
  int kondisi = Firebase.getInt("data/ledStatus");
  Serial.print("data ledStatus = ");
  Serial.println(kondisi);

  //memberikan kondisi led sesuai data ledStatus
  digitalWrite(led, kondisi);

  //baca data sensor 
  float sensor = analogRead(ldr);

  //kirim hasil sensor ke firebase
  Firebase.setFloat("data/sensor", sensor);
  if(Firebase.failed()) {
    //memunculkan pesan error jika gagal
    Serial.println(Firebase.error());  
    return;
  } else {
    //pesan jika sensor berhasil terkirim
    Serial.println("Data sensor berhasil dikirim ke Firebase");
  }

  //jeda
  delay(500); 
  
}
```

Coba upload kode diatas dan bukalah serial Monitor, kemudian amatilah hasilnya.

![serial monitor](https://i.ibb.co/mG6hT2Y/firabasestatus.png)

Selanjutnya bukalah database realtime anda di firebase console. Amatilah hasilnya dan coba ubah nilai **ledStatus** menjadi 1, *Apakah yang terjadi pada rangkaian anda?*

![ubah data](https://i.ibb.co/tqSSDQy/firebase-ubah.png)


Untuk lebih lanjut mengenai library Arduino Firebase bisa ke [https://firebase-arduino.readthedocs.io/en/latest/](https://firebase-arduino.readthedocs.io/en/latest/)

Kita bisa membuat aplikasi client dengan aplikasi Android dengan [Kodular](https://www.kodular.io/) tutorial lengkap bisa ke [sini](https://www.youtube.com/watch?v=qXgdGXzA2EM) dan [sini](https://www.youtube.com/watch?v=_60DhEQA-XI)

Sampai disini kita sudah bisa memanfaatkan platform iot seperti firebase untuk mengembangkan project IoT kita. Untuk aplikasi client bisa menggunakan android atau web dengan menggunakan bahasa pemrograman yang diinginkan.

## Referensi
---

- Prasetya, Rudy Eko: 2019, Modul Pemrograman Dasar C++, CreativeCommon. 
- [https://rudyekoprasetya.wordpress.com/2020/02/27/belajar-iot-internet-of-things-tanpa-punya-alat/](https://rudyekoprasetya.wordpress.com/2020/02/27/belajar-iot-internet-of-things-tanpa-punya-alat/)
- [https://www.arduino.cc/](https://www.arduino.cc/)
- [https://id.wikipedia.org/wiki/Internet_untuk_Segala](https://id.wikipedia.org/wiki/Internet_untuk_Segala)
- [https://auftechnique.com/apa-itu-nodemcu-jenis-papan-sirkuit-iot-30-pin/](https://auftechnique.com/apa-itu-nodemcu-jenis-papan-sirkuit-iot-30-pin/)
- [https://www.cronyos.com/cara-install-driver-ch340-arduino/](https://www.cronyos.com/cara-install-driver-ch340-arduino/)
- [https://www.tutorialiot.com/2019/02/cara-mudah-install-board-esp8266-di.html](https://www.tutorialiot.com/2019/02/cara-mudah-install-board-esp8266-di.html)
- [https://teknikelektronika.com/pengertian-led-light-emitting-diode-cara-kerja/](https://teknikelektronika.com/pengertian-led-light-emitting-diode-cara-kerja/)
- [http://blog.famosastudio.com/2011/06/tutorial/tutorial-breadboard-untuk-arduino/59](http://blog.famosastudio.com/2011/06/tutorial/tutorial-breadboard-untuk-arduino/59)
- [https://id.wikipedia.org/wiki/Resistor](https://id.wikipedia.org/wiki/Resistor)
- [https://medium.com/@andreanewgate/mengkoneksikan-nodemcu-ke-ssid-b7d586ba05c7](https://medium.com/@andreanewgate/mengkoneksikan-nodemcu-ke-ssid-b7d586ba05c7)
- [https://www.warriornux.com/ledcontrol-dengan-webpage-esp8266/](https://www.warriornux.com/ledcontrol-dengan-webpage-esp8266/)
- [https://id.wikipedia.org/wiki/Firebase](https://id.wikipedia.org/wiki/Firebase)
- [https://firebase-arduino.readthedocs.io/en/latest/](https://firebase-arduino.readthedocs.io/en/latest/)
- [https://www.nyebarilmu.com/tutorial-iot-kendali-relay-dengan-esp8266-dan-firebase/](https://www.nyebarilmu.com/tutorial-iot-kendali-relay-dengan-esp8266-dan-firebase/)
- [https://berqas.com/membangun-basic-smart-home-project-menggunakan-konsep-iot-papan-nodemcu-firebase-realtime-database-dan-aplikasi-android/](https://berqas.com/membangun-basic-smart-home-project-menggunakan-konsep-iot-papan-nodemcu-firebase-realtime-database-dan-aplikasi-android/)



## Tentang
---

![Penyusun](https://rudyekoprasetya.files.wordpress.com/2009/10/mine.jpg?w=138)

Syahdan,  Seorang anak laki-laki..  lahir di Tulungagung 02 Desember 1990 tepatnya hari minggu wage, Anak pertama dan terakhir ayah ibu dan ingin sekali belajar sampai ke negara seberang.. (semoga bisa ya…). Kehidupan dimulai saat pendidikan dimulai.. ibu selalu mendidik untuk selalu berbuat baik dan jangan sampai menyakiti hati orang lain, dari TK , SD Ngadirejo 1,  dan SMP Negeri 1 di kediri jawa timur, (Bagaimana klo SMA..??) saya ndak pernah SMA,  dulu bercita-cita jadi dokter namun saya urungkan, karena kondisi ekonomi orang tua yang tidak mendukung, akhirnya saya banting setir putar haluan ke SMK, Saya Lulusan SMK Negeri 1 Kediri (kediri juga..??) . Namun Tuhan itu adil, impian untuk menjadi dokter akhirnya di wujudkan (Loohhh koq bisa..??) karena saya jadi dokter komputer, saya mengambil jurusan Teknik Komputer Jaringan. dan Alhamdulillah Lulus di Tahun 2009.

setelah menuntut ilmu, saya mencoba untuk mengamalkannya… lulus dari SMK saya berkeinginnan untuk kuliah, namun tetap berhadapan dengan masalah klasik, yaitu uang, namun klo ada kemauan pasti ada jalan, alhamdulilah saya bekerja disalah satu toko komputer di kediri, dan berkat itu pula saya bisa mendaftar kuliah PTS dikediri, yaitu Universitas Nusantara PGRI. Banyak hal yang bisa dipetik dalam menghadapi kuliah dan kerja ini, khususnya dalam membagi waktu dan perasaan. Sedikit kesulitan pada Tahun Pertama Alhamdulillah bisa diatasi.

Setelah belajar, Mengamalkan, kemudian ada jalan untuk menyampaikan kepada orang lain. Tepatnya September 2010 saya mengajar, meski masih anak bawang dalam dunia pendidikan namun ndak ada salahnya dicoba, karena belajar yang baik itu adalah belajar untuk menyampaikan ilmu kepada orang lain. Fokus pembelajaran dan riset saya adalah *web development (frontend dan backend), Android Development, Linux SysAdmin, AI (Artificial Intelligent) dan lagi gandrung jua dengan IoT (internet Of Things)*