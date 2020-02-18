# BigData_Tugas1

# Dokumentasi Praktek ETL menggunakan KNIME

* [Business Understanding](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/tugas1/README.md#business-understanding)<br/>
* [Data Understanding](https://github.com/wisnugroho28/BigData_Tugas1/master/tugas1/README.md#data-understanding)<br/>
* [Data Preparation](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/tugas1/README.md#data-preparation)<br/>
* [Modeling](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/tugas1/README.md#modeling)<br/>
  - [Proses membaca data dari dua sumber yang berbeda](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/tugas1/README.md#proses-membaca-data-dari-dua-sumber-yang-berbeda)<br/>
  - [Proses Modeling](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/tugas1/README.md#proses-modeling)<br/>
* [Evaluation](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/tugas1/README.md#evaluation)<br/>
* [Deployment](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/tugas1/README.md#deployment)<br/>

# Business Understanding
Kemungkinan-kemungkinan yg dapat dilakukan yaitu:
1. Dari data tersebut, dapat dilakukan proses untuk melihat map yang paling banyak dimainkan
2. Dari data tersebut, dapat dilakukan proses untuk melihat persentase kill/death
3. Dari data tersebut, dapat dilakukan proses untuk melihat rata-rata lama waktu per permainan

# Data Understanding

- Counter Strike:Global Offensive merupakan salah satu permainan online yang populer selama satu<br/>
  dekade ini. Counter Strike:Global Offensive (CS:GO) merupakan game bergenre FPS <br/>
  (First Person Shooter) yang terdiri dari 2 tim berlawanan (Terrorrists & Counter Terrorrists) <br/>
  yang masing-masing timnya berjumlah 5 orang pemain dan terdiri dari total 30 ronde per <br/>
  permainan. CS:GO sampai sekarang masih dimainkan oleh banyak orang dari segala kalangan usia.<br/>  
  
- dataset ini berisi statistik salah seorang pemain CS:GO amatir dari amerika serikat.

- dataset ini terdiri dari 1133 baris dan 17 kolom
  -Map: Map yang dimainkan oleh pemain <br/>
  -Day: Tanggal (hari) game tersebut dimainkan<br/>
  -Month: Tanggal (bulan) game tersebut dimainkan<br/>
  -Year: Tanggal (tahun) game tersebut dimainkan<br/>
  -Date: Tanggal game tersebut dimainkan<br/>
  -Wait Time(s): Waktu yang digunakan untuk mencari dan menemukan satu permainan<br/>
  -Match Time(s): Waktu yang dibutuhkan untuk menyelesaikan satu permainan<br/>
  -Team A Rounds: Jumlah poin ronde yang berhasil dicapai oleh tim A<br/>
  -Team B Rounds: Jumlah poin ronde yang berhasil dicapai oleh tim B<br/>
  -Ping: Ping rata-rata dalam satu permainan<br/>
  -Kills: Total kill yang berhasil dikumpulkan oleh pemain per permainan<br/>
  -Assists: Assist yang dikumpulkan pemain (Bila memberikan damage >40% tanpa kill) per permainan<br/>
  -Deaths: Total death pemain per permainan<br/>
  -MVP's: Total MVP yang dikumpulkan pemain per permainan (didapat berdasarkan performa pemain)<br/>
  -HS% : Persentase kill yang didapat dengan headshots (tembakan ke kepala)<br/>
  -Points: Total poin yang didapat pemain<br/>
  -Result: Hasil yang didapat pemain di akhir permainan (16 poin pertama menang, 15-15 seri, <16 kalah)<br/>
  <br/>
- Source dataset : https://www.kaggle.com/thesiff/counterstrike

# Data Preparation
- Karena hanya terdiri dari 1 file csv, saya memisahkan isi data dengan node column splitter yang ada di knime.
- Pertama, saya menggunakan node file reader yang tersedia di knime<br/>
![file read](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/fileread.png "fileread")<br/>

- Kedua, klik kanan lalu buka settings dan "browse file .csv yang ingin digunakan, lalu klik ok<br/>
![filereadfind](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/filereadfind.png "filereadfind")<br/>

- Ketiga, Drag node column splitter kedalam workflow, lalu hubungkan dengan node file reader<br/>
![colsplit](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/colsplit.png "colsplit")<br/>

- Keempat, klik kanan pada node column splitter lalu buka settings.<br/>
![colsplitset](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/colsplitset.png "colsplitset")<br/>
  -2 hasil splitter<br/>
      ![colsplit1](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/colsplit1.png "colsplit1")<br/>    
      ![colsplit2](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/colsplit2.png "colsplit2")<br/>
 
-Kelima, simpan salah satu bagian data di database, dan satu bagian lagi di file csv dengan cara:<br/>
 -Database:
  -Gunakan MySQL Connector lalu hubungkan dan setting dengan database yang ingin dipakai<br/>
    ![sqlconn](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/sqlconn.png "sqlconn")<br/>
    ![sqlconnset](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/sqlconnset.png "sqlconnset")<br/>
  -Ambil node DB Writer, lalu hubungkan dengan MySQL Connector dan node Column splitter<br/>
    ![dbwrite](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/dbwrite.png "dbwrite")<br/>
  -Konfigurasi node DB Writer lalu klik ok <br/>
    ![dbwriteset](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/dbwriteset.png "dbwriteset")<br/>
  -Tabel baru sudah ada di phpmyadmin<br/>
    ![phpadmin](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/phpadmin.png "phpadmin")<br/>
 -CSV:
  -Gunakan node CSV Writer<br/>
    ![csvwrite](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/csvwrite.png "csvwrite")<br/>
  -lalu klik kanan untuk melakukan konfigurasi<br/>
    ![csvwriteset](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/csvwriteset.png "csvwriteset")<br/>
  -Pilih output location lalu klik ok, lalu execute<br/>


# Modeling
### Proses membaca data dari dua sumber yang berbeda
#### Proses membaca dari MYSQL
- yang pertama membaca data dari mysql, dengan menggunakan mysql connector nodes dari knime<br/>
 ![sqlconn](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/sqlconn.png "sqlconn")<br/>
- data di mysql seperti dibawah<br/>
 ![phpadmin](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/phpadmin.png "phpadmin")<br/>
- melakukan configurasi disesuaikan dengan mysql yang ada di phpmyadmin, mulai dari database, port dari localhost dan username.<br/>
 ![sqlconnset](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/sqlconnset.png "sqlconnset")<br/>
- db table selector untuk mengambil Koneksi DB sebagai input dan memungkinkan untuk memilih tabel atau tampilan dari dalam database yang terhubung.<br/>
 ![tabsel](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/tabsel.png "tabsel")<br/>
- db reader untuk Mengeksekusi kueri input dalam database dan mengambil hasilnya ke dalam tabel data KNIME.<br/>
 ![dbread](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/dbread.png "dbread")<br/>
- hasil akhir dari pembacaan database yang terhubung dari mysql<br/>
 ![dbreadnew](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/dbreadnew.png "dbreadnew")<br/>

#### Proses membaca dari csv
- memasang csv reader untuk membaca file csv<br/>
 ![fileread](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/fileread.png "fileread")<br/>
- melakukan konfigurasi , menentukan path file dimana csv disimpan<br/>
 ![filereadfind](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/filereadfind.png "filereadfind")<br/>


### Proses Modeling
- menggunakan joiner node, dengan mengsambungkan node dari database yang mengolah mysql dan csv<br/>
 ![joiner](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/joiner.png "joiner")<br/>
- melakukan configure dengan memilih kolom yang urutan nya sama<br/>
  -hasilnya seperti ini<br/>


- menggunakan column filter untuk menentukan column mana yang mau ditampilkan<br/>
 ![alt text](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/colfilt.png "colfilt" ) <br/>
- hasil akhir<br/>
 ![colfiltres](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/colfiltres.png "colfiltres")<br/>


# Evaluation

- dari kedua data yang ada di mysql dan csv telah berhasil di join

- hasil join


- data asli 


- tes berhasil karena hasil join sama dengan data asli sebelum dipisah

# Deployment
### simpan ke csv
- data yang pertama akan disimpan ke csv dengan menggunakan csv writer<br/>
![csvwrite](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/csvwrite.png "csvwrite")<br/>

- memilih penempatan dan konfigurasi lain nya
![csvwritefinale](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/csvwritefinale.png "csvwritefinale")<br/>
 
- data berhasil tersimpan


 ### simpan ke db
- data akan disimpan ke database menggunakan db writer<br/>
![dbwrite](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/dbwrite.png "dbwrite")<br/>

- memilih konfigurasi lain nya, seperti nama dan db yang dituju<br/>
![dbwritefinale](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/dbwritefinale.png "dbwritefinale")<br/>

- berhasil tersimpan<br/>
![phpadmfinale](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/phpadmfinale.png "phpadmfinale")<br/>

 ### gambar knime secara lengkap
-Preparation Phase<br/>
![prep](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/prep.png "prep")<br/>
-Modelling Phase<br/>
![schemefinale](https://github.com/wisnugroho28/BigData_Tugas1/blob/master/ssimg/schemefinale.png "schemefinale")<br/>


