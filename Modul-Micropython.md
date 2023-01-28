# Modul Praktikum IoT dengan Micropython
---

Penyusun **Rudy Eko Prasetya, S.Kom** - Blog [https://rudyekoprasetya.wordpress.com](https://rudyekoprasetya.wordpress.com/about)

![Pengenalan IoT](https://upload.wikimedia.org/wikipedia/commons/4/4e/Micropython-logo.svg)

Modul ini disusun sebagai bahan ajar praktikum Internet of Things(IoT) Dasar untuk siswa atau Mahasiswa dengan menggunakan bahasa pemrograman Python khususnya micropython. Modul ini disusun berdasarkan dokumentasi resmi Micropython di [http://docs.micropython.org/en/latest/](http://docs.micropython.org/en/latest/)

Modul ini menggunakan lisensi [Creative Common](https://creativecommons.org/licenses/by-sa/4.0/) dengan atribut NonKomersial-BerbagiRupa dimana Lisensi ini mengizinkan setiap orang untuk menggubah, memperbaiki, dan membuat ciptaan turunan bukan untuk kepentingan komersial, selama mereka mencantumkan kredit dan melisensikan ciptaan turunan dengan syarat yang serupa dengan ciptaan asli.

Modul ini dibuat dengan menggunakan [Markdown](https://www.markdownguide.org/) dan akan terus di update seiring dengan pengalaman belajar dan mengajar penyusun. History perubahan atau pull request bisa diakses pada [https://github.com/rudyekoprasetya/LearningArduino](https://github.com/rudyekoprasetya/LearningArduino)

## Daftar Isi
---

- [Pengantar Teknologi IoT](#pengantar-teknologi-iot)
- [Mengenal Mikrokontroller NodeMCU](#mengenal-mikrokontroller-nodemcu)
- [Tentang Micropython](#tentang-micropython)
- [Persiapan dan Installasi](#persiapan-dan-installasi)
- [Membuat LED Blynking](#membuat-led-blynking)
- [Penanganan Digital Input](#penanganan-digital-input)
- [Penanganan Analog Input](#penanganan-analog-input)
- [Penggunaan Sensor Suhu DHT11](#penggunaan-sensor-suhu-dht11)
- [Penggunaan Sensor Jarak](#penggunaan-sensor-jarak) 
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

## Tentang Micropython
---

![micropython](https://docs.ghielectronics.com/software/micropython/images/micropython.png)

**MicroPython** adalah python versi ringan yang memang ditujukan untuk mikrokontroler, sehingga banyak pustaka dan fungsi yang biasa ada pada Python tidak akan didukung untuk MicroPython, sehingga praktis tidak semua grammar dalam Python bisa diaplikasikan untuk MicroPython.

Micropython berjalan diatas **bare-meta** mikrokontroler secara langsung, tidak seperti Python yang memang dirancang berjalan diatas sistem operasi. Beberapa optimasi dibuat guna membuat micropython dapat berjalan pada perangkat dengan resource yang terbatas.

Kelebihan MicroPython ini, kode program ditulis dalam file berekstensi .py dan dapat langsung disimpan di dalam flash memory pada Python board. Proses compiling dilakukan langsung di dalam microprocessor sehingga tidak diperlukan software downloader pada PC. Hal ini sangat memudahkan proses pembuatan dan uji coba program. Selain itu, Micro Python juga dilengkapi dengan **REPL (Read Evaluate Print Loop)** atau *interactive prompt* yang memungkinkan kita untuk mengakses langsung board, mencoba-coba kode program dan melihat hasilnya saat itu juga.

Micro Python adalah proyek yang mendapat pendanaan melalui Kickstarter dan sudah melampaui inisiasi pendanaan sejak bulan Desember 2013. Damien menjadikan Micro Python dan Micro Python board sebagai open source software dan open source hardware di bawah lisensi MIT sehingga siapapun dapat menggunakan, memodifikasi dan memproduksi baik untuk tujuan komersial maupun non-komersial. Semua resource baik itu kode maupun skema board dapat diakses di https://github.com/micropython/. Micro Python juga memiliki forum komunitas yang aktif dengan para programmer yang antusias mengembangkan dan melengkapi library yang ada untuk berbagai keperluan hardware.


## Persiapan dan Installasi
---

Dalam Modul ini karena kita akan menggunakan Mikrokontroller NodeMCU Untuk itu membutuhkan driver dan software pendukung seperti :

1. Python minimal versi 3.7.x, bisa [download disini](https://www.python.org/downloads/) 
2. Untuk Windows 10 Yang stabil versi 3.3.x bisa [download disini](https://thonny.software.informer.com/download/?ca225eb9). Untuk Thonny IDE Terbaru (Micropython) bisa [didownload disini](https://thonny.org/)
3. Driver NodeMCU CH340 [download disini](https://sparks.gogo.co.nz/ch340.html)
4. Firmware Micropython For ESP8266 [download disini](https://micropython.org/download/esp8266/)

Silahkan download dan install software diatas.

### Cara Install Thonny IDE Windows 

1. Setelah Download Lakukan installasi pada file **thonny.exe**

2. Ikuti instruksi dan klik Next untuk melanjutkan installasi
![install](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2019/01/6-Install-Thonny-Windows.png)

3. Tunggu sampai selesai berikut adalah tampilan aplikasi Thonny IDE 
![ide](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2019/01/8-Install-Thonny-Windows.png)

### Cara Install Thonny Linux

1. Disini saya menggunakan distro ubuntu linux, untuk distro lain silahkan merujuk ke [https://thonny.org/](https://thonny.org/)

2. pastikan python sudah terinstall dalam sistem anda. Cek dengan perintah 

```console
python --version
```
atau

```console
python3 --version
```

3. Untuk Install ketikan perintah

```console
pip install thonny
```

atau untuk python3

```console
pip3 install thonny
```

4. Tunggu sampai installasi selesai, untuk menjalankan gunakan perintah

```console
thonny
```

### Cara Install driver CH340
1. Setelah Mendowload driver CH340 silahkan extract dan jalankan file **setup.exe**

![install diver ch40](https://2.bp.blogspot.com/-QyVEUUba9PM/Wd83wY73GqI/AAAAAAAADWA/QDWkg1SaAe8CJpGyoJXk9jJGShcQSKKIwCK4BGAYYCw/s1600/path_ch340g_setup.jpg)

2. Selanjutnya langsung klik install
![install driver](https://2.bp.blogspot.com/-TtCCSUHce7g/Wd84GGO8RoI/AAAAAAAADWM/gLRFWKuJWOgP8xUfuqe5d_NVRbUwkYDwwCK4BGAYYCw/s1600/ch340g_install_window.jpg)

3. Koneksikan NodeMCU dengan komputer atau laptop anda via kabel USB. Kemudian buka **Device Manager** dan pastikan pada bagian **Port(COM&LPT)** sudah terinstall diver CH340
![device manager](https://3.bp.blogspot.com/-3n5Kk7N1o8c/Wd84ULu9aJI/AAAAAAAADWU/qynH3m2ju04iVUYR2h8IW9OHYeA8-RJEwCK4BGAYYCw/s1600/ch340g_installed_successfully.jpg)

**Amati dan perhatikan nilai COM pada device manager tersebut, dicontoh adalah COM19 hal ini biasanya berbeda pada setiap komputer atau laptop**

### Install Firmware Board ESP8266 di Thonny IDE
1. Pastikan komputer atau laptop terhubung dengan internet kemudian buka Aplikasi Arduino IDE yang sudah di install sebelumnya

2. Pastikan sudah download firmwarenya di situs [https://micropython.org/download/esp8266/](https://micropython.org/download/esp8266/). Anda akan mendownload file **esp8266-20220618-v1.19.1.bin**, ingat tempat downloadnya.

3. Koneksikan Board NodeMCU anda ke laptop/komputer

4. Buka Thonny IDE, masuk menu **Tools > Opstions > Interpreter**

5. Pada *Which interpreter or device should Thonny use*, pilih MicroPython ESP8266, pilih pula COM port sesuai dengan yang ada pada device manager. Selanjutnya klik **install or update firmware**
![thonny1](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2019/01/flash-micropython-firmware-thonny-ide-1.png)

6. Pilih port COM nya, kemudian klik **Browse** untuk mengarahkan ke file firmware yang sudah terdownload tadi. Jika sudah klik **Install**
![thonny2](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2019/01/ESP-firmware-installer-thonny-ide.png)

7. Tunggu sampai proses selesai, Close jendela update firmaware. Jika installasi berhasil maka pada shell prompt akan muncul boardnya
![thonny3](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2019/01/3-thonny-ide-window-generic-micropython.png)


8. Coba ketikan perintah `help()` untuk melihat respon detail bord yang terkoneksi
![thonny4](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2019/01/thonny-help.png)


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

```python
#import library microcontroller
from machine import Pin
#import untuk jeda
from time import sleep
led = Pin(14, Pin.OUT) #setting pin GPIO mode OUTPUT
while True:
  led.on() 
  sleep(1) 
  led.off() 
  sleep(1) 
```

Klik menu **File > Save As** maka akan muncul tampilan dibawah ini

![save](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2019/01/save-micropython-device-thonny-ide.png)

Jika ingin menyimpan di laptop atau komputer silahkan pilih **This Computer**, semisal kita simpan code tersebut di *Documents/BelajarMicropython/Belajar1/* dengan nama file **main.py**

Atau jika ingin langsung di eksekusi id board kita pilih **MicroPython device**, berikan nama file **main.py**, agar bisa langsung di jalankan saat device menyala.

![save as](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2022/01/save-main-py-thonny-device.png)

Seharusnya sudah ada file **boot.py** yang secara otomatis sudah ada saat menginstall firmware. Klik tombol **OK**, maka secara otomatis akan menyimpan dalam device.

Klik tombol RST/EN pada device untuk menjalankannya. Tunggu sampai proses selesai dan Amatilah LED Anda. 

Coding `led = Pin(14, Pin.OUT)` digunakan untuk konfigurasi PIN yang digunakan, dikarenakan kita gunakan D5, maka sesuai dengan GPIO ny NodeMCU yaitu GPIO14. Sedangkan  Coding `led.on()` digunakan untuk mengirim data digital ke PIN untuk mengontrol LED baik ON yang berarti menyala atau OFF berati mati.

Selanjutnya ubah codenya menjadi dibawah ini

```python
#import library microcontroller
from machine import Pin
#import untuk jeda
from time import sleep
led = Pin(14, Pin.OUT) #setting pin GPIO mode OUTPUT
while True:
  led.value(0)
  sleep(0.5) 
  led.value(1)
  sleep(0.5) 
```
Coba upload kembali code diatas ke NodeMCU anda dengan menekan panah hijau atau tombol keyboard **F5** dan amatilah hasilnya

Untuk menghentikan eksekusi program tekan tombol stop atau shortcut **CTRL + F2**

Selanjutnya ubah kode diatas menjadi dibawah ini

```python
#import library PWM
from machine import Pin,PWM
#import untuk jeda
from time import sleep

led = PWM(Pin(14), freq=5000) #setting pin GPIO mode OUTPUT untuk PWM

while True:
  for cycle in range(0, 1024):
    led.duty(cycle)
    sleep(0.005)
```

simpan ke microcontroller dan jalankan code diatas, *apakah yang terjadi pada led??*

**PWM** atau *Pulse Width Modulation* adalah suatu teknik modulasi yang mengubah lebar pulsa (pulse width) dengan nilai frekuensi dan amplitudo yang tetap. PWM dapat dianggap sebagai kebalikan dari ADC (Analog to Digital Converter) yang mengkonversi sinyal Analog ke Digital, PWM atau Pulse Width Modulation ini digunakan menghasilkan sinyal analog dari perangkat Digital.

Sinyal PWM akan tetap ON untuk waktu tertentu dan kemudian terhenti atau OFF selama sisa periodenya. Yang membuat PWM ini istimewa dan lebih bermanfaat adalah kita dapat menetapkan berapa lama kondisi ON harus bertahan dengan cara mengendalikan siklus kerja atau **Duty Cycle** PWM.

Frekuensi sinyal PWM menentukan seberapa cepat PWM menyelesaikan satu periode. Satu Periode adalah waktu ON dan OFF penuh dari sinyal PWM. Sederhananya, seberapa cepat sinyal PWM harus dihidupkan (ON) dan dimatikan (OFF) ditentukan oleh frekuensi sinyal PWM dan kecepatan berapa lama sinyal PWM harus tetap ON (hidup) ditentukan oleh Duty Cycle sinyal PWM.

Dengan PWM ini kita bisa mengatur output sinyal digital dari Pin NodeMCU sesuai dengan kebutuhan. Semisal digunakan untuk mengatur kecepatan kipas, kecerahan lampu atau lainnya.


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

dalam Rangkaian tersebut PIN yang digunakan adalah PIN D7(GPIO 13) untuk LED Hijau kemudian PIN D8 (GPIO 15) untuk PushButton dan PIN 3.3 V untuk arus ke Push button beserta PIN GND untuk groundnya.

Selanjutnya buka Thonny IDE buat file baru dan ketikan kode dibawah ini

```python
from machine import Pin
from time import sleep

tombol = Pin(15, Pin.IN)

while True:
    print('Hasil tombol =', tombol.value())
    sleep(0.5)
```

Kita sudah mengetahui bahwa untuk pinMode dari LED adalah OUTPUT Namun beda dengan push button yaitu pinMode yang digunakan adalah INPUT untuk itu codenya `tombol = Pin(15, Pin.IN)`. Kita cetak hasil tombol ke shell dengan code `print('Hasil tombol =', tombol.value())`.

Selanjutnya simpan code diatas dengan nama file **main.py** difolder *belajar2*. Jangan lupa Hubungkan NodeMCU dengan komputer atau laptop via USB

Hubungkan NodeMCU dengan komputer atau laptop via USB Untuk verifikasi code. Selanjutnya langsung upload dengan klik **tombol Panah hijau** di sebelahnya.

Cobalah tekan tombol dan lepas tombol dan amatilah hasil yang ditampilkan pada shell dibawah.

Disini kita bisa amati bahwa bila tombol ditekan akan mengirimkan nilai 1 sedangkan bila dilepas akan mengirimkan hasil 0.

Ubahlah kode menjadi dibawah ini

```python
from machine import Pin
from time import sleep

tombol = Pin(15, Pin.IN)
led = Pin(13, Pin.OUT)

while True:
    print('Hasil tombol =', tombol.value())
    led.value(tombol.value())
    sleep(0.5)
```

Coba upload kembali ke NodeMCU Anda kemudian tekan push buttonnya. *Apakah yang terjadi??*

Selain menangani digital input dari saklar atau push button, kita jua bisa mengelola input dari keyboard komputer atau laptop yang tersambung dengan NodeMCU.

Coba buat rangkaian sederhana 1 LED seperti bab sebelumnya.
![Rangkaian Led](https://i.ibb.co/9Yq8SJz/iot1.jpg)

Kemudian ketikan kode dibawah ini

```python
from machine import Pin
from time import sleep

led = Pin(13, Pin.OUT)

while True:
    keyboard=input('Masukan Angka 1 atau 2 ')
    if(keyboard == "1"):
        led.on()
    else:
        led.off()
```

Untuk nomor pin disini menggunkan pin D7(GPIO 13) untuk led Merah.  Kode `keyboard=input('Masukan Angka 1 atau 2 ')` digunakan untuk menampung input user saat menekan tombol keyboard dan disimpan dalam variabel *keyboard*. Tiap input keyboard yang dibaca akan dibandingkan dengan struktur percabangan if untuk control LED.

Simpan kode diatas dengan nama **keyboard.py** dikomputer anda selanjutnya upload code anda dan ketikan angka 1 kemudian tekan enter. Amatilah hasilnya.

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

Pada rangkaian diatas sensor LDR mendapatkan tegangan dari pin 3.3 V dan GND kemudian diberikan resistor di jalur GND. Pin Analog A0 di letakknya salah satu pin sensor yang akan digunakan untuk membaca hasil sensor. Kemudian di pasang LED di PIN D1 (GPIO 5).

Untuk codenya adalah sebagai berikut ini

```python
from machine import Pin, ADC
from time import sleep

sensor = ADC(0)
led = Pin(5, Pin.OUT)

while True:
    print('Hasil sensor= ', sensor.read())

    if(sensor.read() < 100):
        led.on()
    else:
        led.off()

    sleep(0.5)
```  

Untuk konfigurasi pada kode `led = Pin(13, Pin.OUT);` digunakan untuk konfigurasi LED di pin D1 sedangkan kode `sensor = ADC(0)` untuk konfigurasi pin A0. Kode `print('Hasil sensor= ', sensor.read())` digunakan untuk menampung nilai hasil pembacaan sensor kedalam variabel hasil.

Pada struktur percabangan kode `if(sensor.read()<100)` adalah untuk kondisi dimana LED akan menyala atau mati. Silahkan diatur sesuai dengan keinginan dan
itensitas cahaya yang diinginkan. angka 10 diperoleh dari pembacaan nilai dari sensor dimana ada jumlah arus listrik yang dibaca sensor, jika cahaya kurang maka nilai akan rendah sebaliknya jika cahaya intensitas tinggi maka nilai akan naik. 

Simpan kode diatas dengan nama **main.py** di folder *Belajar3* Untuk menguji hasil silahkan upload kode diatas. Cobalah untuk menutup sensor agar intensitas cahaya berkurang dan amatilah hasilnya.

### latihan
1. Buatlah Rangkaian IoT untuk prototipe smart traffic light dengan ketentuan
    - Terdapat 3 LED (misal merah, kuning, hijau)
    - Jika kondisi siang / banyak cahaya maka Led akan menyala bergantian dengan ketentuan
        - LED merah menyala selama 3 detik
        - Kemudian LED kuning menyala selama 1 detik
        - Dilanjutkan LED hijau menyala selama 2 detik
    - Jika kondisi malam / sedikit cahaya maka yang menyala hanya LED kuning secara berkedip kedip

## Penggunaan Sensor Suhu DHT11
---

![dht11](https://www.ardutech.com/wp-content/uploads/2019/10/30.-DHT11-1.jpg)

**DHT11** adalah salah satu sensor yang dapat mengkur dua parameter lingkungan, yaitu suhu (Temperature) dan kelembaban (Humidity). Dalam sensor ini terdapat sebuah thermistor NTC (Negative Temperature Coefficient) untuk mengukur suhu, sebuah sensor kelembaban tipe resisitif dan sebuah mikrokontroller 8 bit yang mengolah kedua sensor tersebut untuk mengirimkan hasil sensor. 

Keunggulan dari sensor DHT11 dibanding dengan yang lainnya antara lain memiliki kualitas pembacaan data sensing yang sangat baik, responsif (cepat dalam pembacaan kondisi ruangan) serta tidak mudah terinterferensi.

Untuk praktikum siapkan
- NodeMCU 1x
- Breadboard 1x
- DHT11 1x
- Kabel Jumper

Rangkailah seperti gambar dibawah ini
![suhu](https://miro.medium.com/max/585/0*D8-J3qyLf94VJzA7.png)

berikut adalah codenya

```python
from machine import Pin
from time import sleep
import dht

sensor = dht.DHT11(Pin(14))


while True:
    sensor.measure()
    print("suhu =",sensor.temperature())
    print("kelembaban = ",sensor.humidity())
    sleep(0.5)

```

Simpan dengan nama file **main.py** dan simpan dalam nodeMCU anda. jalankan codenya dengan menekan tombol F5, kemudian amatilah hasilnya


## Penggunaan Sensor Jarak
---

**Sensor ultrasonik** adalah sebuah sensor yang memiliki fungsi untuk mengubah besaran fisis alias bunyi menjadi besaran listrik, begitupun sebaliknya. Prinsip kerja sensor ultrasonik ini cukup simpel, yakni berdasarkan pantulan suatu gelombang suara sehingga dapat digunakan untuk mendefiniskan eksistensi atau jarak suatu benda dengan frekuensi tertentu. 

*Mengapa disebut sensor ultrasonik?* Karena sensor ini menggunakan gelombang ultrasonik. Gelombang ultrasonik sendiri memiliki frekuensi yang sangat tinggi, mencapai 20.000 Hz yang tidak bisa didengar oleh telinga manusia. Bunyi dengan frekuensi setinggi itu hanya bisa didengar oleh hewan-hewan tertentu seperti kucing, anjing, kelelawar, sampai dengan lumba-lumba.

![jarak](https://1.bp.blogspot.com/-A-WzAUJMmXE/X6wRJoaqYBI/AAAAAAAAEjc/Kp-KvuED9Zc4XFBnIM_Qaw-LOnd9bnYWwCNcBGAsYHQ/w0/hc-sr04%2B%2B.jpg)

Secara sederhana, sensor ultrasonik akan menembakkan gelombang ultrasonik (*trigger*) menuju objek tertentu. Setelah gelombang menyentuh objek, maka gelombang akan dipantulkan kembali ke sensortersebut, lalu sensor akan menghitung selisih antara waktu pengiriman dan waktu penerimaan gelombang pantul (*echo*).

Siapkan komponen berikut ini

- NodeMCU 1x
- BreadBoard 1x
- Sensor HR-SC04 1x
- Kabel Jumper

Rangkailah seperti gambar dibawah ini

![jarak2](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2021/06/ESP8266-Ultrasonic-Sensor-Wiring-Fritzing-Diagram.png)

pertama kita membutuhkan library untuk pembacaan sensor, silahkan buat file baru dengan nama **hcsr04.py** berikut codenya

```python
import machine, time
from machine import Pin

__version__ = '0.2.0'
__author__ = 'Roberto Sánchez'
__license__ = "Apache License 2.0. https://www.apache.org/licenses/LICENSE-2.0"

class HCSR04:

    def __init__(self, trigger_pin, echo_pin, echo_timeout_us=500*2*30):
        
        self.echo_timeout_us = echo_timeout_us

        self.trigger = Pin(trigger_pin, mode=Pin.OUT, pull=None)
        self.trigger.value(0)

        self.echo = Pin(echo_pin, mode=Pin.IN, pull=None)

    def _send_pulse_and_wait(self):
        self.trigger.value(0) # Stabilize the sensor
        time.sleep_us(5)
        self.trigger.value(1)
        # Send a 10us pulse.
        time.sleep_us(10)
        self.trigger.value(0)
        try:
            pulse_time = machine.time_pulse_us(self.echo, 1, self.echo_timeout_us)
            return pulse_time
        except OSError as ex:
            if ex.args[0] == 110: # 110 = ETIMEDOUT
                raise OSError('Out of range')
            raise ex

    def distance_mm(self):
        pulse_time = self._send_pulse_and_wait()
        mm = pulse_time * 100 // 582
        return mm

    def distance_cm(self):
        pulse_time = self._send_pulse_and_wait()
        cms = (pulse_time / 2) / 29.1
        return cms
```
simpan dalam device anda, selanjutnya kita buat file **main.py**

```python
from hcsr04 import HCSR04
from time import sleep

sensor = HCSR04(trigger_pin=12, echo_pin=14, echo_timeout_us=10000)

while True:
    jarak = sensor.distance_cm()
    print('Jaraknya adalah ', jarak, 'cm')
    sleep(1)
```

Jalankan code diatas dan amatilah hasilnya

## Koneksi Dengan WiFi
---

Seperti yang sudah kita ketahui bahwa NodeMCU berbasiskan Chip ESP8266 dimana sudah ada modul WiFi didalamnya. Sehingga kita bisa menghubungkanya dengan jaringan seperti jaringan internet.

Untuk praktikum bukalah Thonny IDE anda dan buat file baru, ketikan code dibawah ini

```python
def do_connect():
    import network
    wlan = network.WLAN(network.STA_IF)
    wlan.active(True)
    if not wlan.isconnected():
        print('sedang mengkoneksikan...')
        wlan.connect('SSID', 'wifi password')
        while not wlan.isconnected():
            pass
    print('Konfigurasi Network Anda :', wlan.ifconfig())

do_connect()
```

Simpan dengan nama **main.py** difolder *belajar5* kemudian upload ke NodeMCU anda. Kemudian amatilah apa yang muncul.

Jika berhasil maka pada serial monitor akan muncul IP address yang terkoneksi pada SSID. 

Jika anda ingin mengkoneksikan ulang Cukup ditekan tombol **RST** pada NodeMCU maka secara otomatis akan mencari koneksi ke hotspot yang sudah di daftarkan.


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



Sampai disini kita sudah bisa memanfaatkan platform iot untuk mengembangkan project IoT kita.

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
- [https://miqbal.staff.telkomuniversity.ac.id/micropython/](https://miqbal.staff.telkomuniversity.ac.id/micropython/)
- [https://randomnerdtutorials.com/getting-started-thonny-micropython-python-ide-esp32-esp8266/](https://randomnerdtutorials.com/getting-started-thonny-micropython-python-ide-esp32-esp8266/)
- [https://docs.micropython.org/en/latest/esp8266/quickref.html](https://docs.micropython.org/en/latest/esp8266/quickref.html)
- [https://randomnerdtutorials.com/micropython-gpios-esp32-esp8266/](https://randomnerdtutorials.com/micropython-gpios-esp32-esp8266/)
- [https://randomnerdtutorials.com/micropython-hc-sr04-ultrasonic-esp32-esp8266/](https://randomnerdtutorials.com/micropython-hc-sr04-ultrasonic-esp32-esp8266/)
-[https://yungger.medium.com/so-easy-micropython-mqtt-thingspeak-iot-8c344fa23517](https://yungger.medium.com/so-easy-micropython-mqtt-thingspeak-iot-8c344fa23517)


## Tentang
---

![Penyusun](https://rudyekoprasetya.files.wordpress.com/2009/10/mine.jpg?w=138)

Syahdan,  Seorang anak laki-laki..  lahir di Tulungagung 02 Desember 1990 tepatnya hari minggu wage, Anak pertama dan terakhir ayah ibu dan ingin sekali belajar sampai ke negara seberang.. (semoga bisa ya…). Kehidupan dimulai saat pendidikan dimulai.. ibu selalu mendidik untuk selalu berbuat baik dan jangan sampai menyakiti hati orang lain, dari TK , SD Ngadirejo 1,  dan SMP Negeri 1 di kediri jawa timur, (Bagaimana klo SMA..??) saya ndak pernah SMA,  dulu bercita-cita jadi dokter namun saya urungkan, karena kondisi ekonomi orang tua yang tidak mendukung, akhirnya saya banting setir putar haluan ke SMK, Saya Lulusan SMK Negeri 1 Kediri (kediri juga..??) . Namun Tuhan itu adil, impian untuk menjadi dokter akhirnya di wujudkan (Loohhh koq bisa..??) karena saya jadi dokter komputer, saya mengambil jurusan Teknik Komputer Jaringan. dan Alhamdulillah Lulus di Tahun 2009.

setelah menuntut ilmu, saya mencoba untuk mengamalkannya… lulus dari SMK saya berkeinginnan untuk kuliah, namun tetap berhadapan dengan masalah klasik, yaitu uang, namun klo ada kemauan pasti ada jalan, alhamdulilah saya bekerja disalah satu toko komputer di kediri, dan berkat itu pula saya bisa mendaftar kuliah PTS dikediri, yaitu Universitas Nusantara PGRI. Banyak hal yang bisa dipetik dalam menghadapi kuliah dan kerja ini, khususnya dalam membagi waktu dan perasaan. Sedikit kesulitan pada Tahun Pertama Alhamdulillah bisa diatasi.

Setelah belajar, Mengamalkan, kemudian ada jalan untuk menyampaikan kepada orang lain. Tepatnya September 2010 saya mengajar, meski masih anak bawang dalam dunia pendidikan namun ndak ada salahnya dicoba, karena belajar yang baik itu adalah belajar untuk menyampaikan ilmu kepada orang lain. Fokus pembelajaran dan riset saya adalah *web development (frontend dan backend), Android Development, Linux SysAdmin, AI (Artificial Intelligent) dan lagi gandrung jua dengan IoT (internet Of Things)*