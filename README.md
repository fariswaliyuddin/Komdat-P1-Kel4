<h1 align="center"><img src="images/logo.png" width=400></h1>


[Instalasi](#instalasi) | [Konfigurasi](#konfigurasi) | [Otomatisasi](#otomatisasi) | [Cara Penggunaan](#cara-penggunaan) | [Pembahasan](#pembahasan) | [Referensi](#referensi)
:---:|:---:|:---:|:---:|:---:|:---:


# KooZic
Koozic adalah layanan streaming musik berbasis server yang ada pada aplikasi Odoo. KooZic memungkinkan penggunanya untuk mengakses koleksi musik mereka dimanapun dan dari perangkat apapun.

## Instalasi

1. Membuat Spesifik User
    Untuk alasan keamanan, disarankan membuat user dan tidak memakai user root. Contohnya seperti `koozic`.
2. Install Prasyarat
    Sebelum instalasi, pastikan semua package dan pip dependencies sudah terpasang. Berikut packages yang dimaksud:
    - Untuk DEB-based OS: [apt packages](https://github.com/DocMarty84/koozic_install/blob/fdc1649538d75675cfebe4cf4f6ab6fb88eea62c/koozic_install.py#L268-L309), [pip packages](https://github.com/DocMarty84/koozic_install/blob/fdc1649538d75675cfebe4cf4f6ab6fb88eea62c/koozic_install.py#L312-L315)
    - Untuk RPM-based OS: [dnf packages](https://github.com/DocMarty84/koozic_install/blob/fdc1649538d75675cfebe4cf4f6ab6fb88eea62c/koozic_install.py#L327-L381), [extra pip packages](https://github.com/DocMarty84/koozic_install/blob/fdc1649538d75675cfebe4cf4f6ab6fb88eea62c/koozic_install.py#L384-L387)

    pip digunakan untuk menginstall dependencies (bukan menggunakan package manager)

3. Set-up PostgreSQL
    Selanjutnya set-up PostgreSQL. Asumsikan kita akan menjalankan KooZic dengan nama user koozic, maka kita perlu membuat user PosrgreSQL seperti ini
    ```sh
    su - postgres -c "createuser -s koozic"
    ```
4. Download KooZic
    Setelah setup PostgreSQL, download versi terbaru dari KooZic menggunakan file `koozic-*.tar.gz` lalu uncompress arsip yang telah didownload
5. Launch KooZic
    Terakhir, eksekusi skrip dibawah ini sebagai user `koozic` : 
    ```sh
    ./odoo-bin --workers=4 -d koozic-v3 --limit-time-cpu=1800 --limit-time-real=3600 --without-demo=all --no-database-list
    ```
    Jika menggunakan Fedora, tambahkan skrip ``--db-template=template0`` ke command line. Hal ini juga mungkin berlaku di tipe distribusi yang lain.
    
    Setelah 10-20 detik launching dan pemasangan database, kita dapat menggunakan KooZic di alamat http://localhost:8069 dengan email/password `admin` .

## Konfigurasi

## Otomatisasi
1. Instalasi
    Di terminal, jalankan skrip berikut:
    ```sh
    wget https://raw.githubusercontent.com/DocMarty84/koozic_install/v3/koozic_install.py -O koozic_install.
    ```
    ```sh
    sudo python3 koozic_install.py install
    ```
    Kemudian akses KooZic pada browser Anda di http://localhost:8069 dengan default login dan password nya adalah `admin`. Jangan lupa untuk mengganti password setelah instalasi.
    
2. Uninstalasi
   Untuk uninstalling, jalankan skrip berikut:
   ```sh
   sudo python3 koozic_install.py uninstall
   ```
   Uninstalasi tidak termasuk penghapusan data pada PostgreSQL, untuk itu remove FFMpeg yang ada pada direktori `/usr/local/bin/ffmpeg`
    Untuk uninstalling, jalankan skrip berikut:
    ```sh
    sudo python3 koozic_install.py uninstall
    ```
    Uninstalasi tidak termasuk penghapusan data pada PostgreSQL, untuk itu remove FFMpeg yang ada pada direktori `/usr/local/bin/ffmpeg`
    
## Cara Penggunaan

Karna fungsionalitas sistemnya yang bisa dibilang cukup minimum, website koozic ini dinilai cukup mudah untuk digunakan. Cara penggunaan website ini adalah sebagai berikut:

1. Pengguna diharuskan login untuk dapat menggunakan layanan. Untuk pengguna baru dapat menggunakan email dan password **admin**.

<p align="center">
    <img src="images/login.png" width="700">
</p>

2. Setelah login berhasil, user akan masuk ke halaman dashboard musik. Disini user dapat melihat album ataupun musik yang telah dimasukan ke dalam sistem. User dapat memainkan musik yang diinginkan atau memasukkannya ke dalam playlist yang dapat diakes melalui menu navigasi.


<p align="center">
    <img src="images/home.png" width="700">
</p>

3. Untuk dapat memasukan music atau video ke dalam sistem, pengguna terlebih dahulu harus melakukan konfigurasi folder dengan mengakses *configuration folder * pada menu navigasi.

<p align="center">
    <img src ="images/menu.png">
</p>

4. Di halaman configuration pengguna dapat menambahkan **path** baru dimana sistem akan secara otomatis dapat melakukan scanning **path** tersebut untuk mendeteksi file musik / video.

<p align="center">
    <img src ="images/folder.png" width="700">
</p>

5. Tampilan saat melakukan konfigurasi path adalah sebagai berikut.

<p align="center">
    <img src ="images/edit-folder.png" width="700">
</p>

6. Selain memutar musik. User juga dapat memutar video pada sistem ini. Untuk mengaksesnya user dapat membuka melalui menu navigasi di kiri atas.

<p align="center">
    <img src ="images/nav.png">
</p>

7. Tampilan saat memutar video adalah sebagai berikut.

<p align="center">
    <img src="images/video-play.png" width="700">
</p>

8. Admin dapat menambahkan user baru dan memberikan akses tertentu kepada user tersebut melalui halaman *settings*.

<p align="center">
    <img src="images/setting.png" width="700">
</p>

## Pembahasan
### Free & Open-Source
Mengandalkan Odoo, diterbitkan di bawah lisensi LGPL, OOMusic dan OOVideo, diterbitkan di bawah lisensi MIT.
### Search Thanks to ID3 Tags
Tag ID3 memungkinkan Anda mengatur musik dengan mudah. Temukan dengan cepat apa yang Anda cari: judul lagu, album, artis, atau genre! KooZic menyediakan fungsionalitas pencarian yang kuat.
### Enjoy Powerful Playlists
Buat daftar putar Anda dalam beberapa detik! Tambahkan lagu, album, atau bahkan seluruh koleksi artis ke daftar putar Anda hanya dengan satu klik!
### Any music or video format
Media di-transcoding dengan cepat! MP3? OGG? FLAC? MKV? Tidak masalah: KooZic menangani semuanya berkat FFmpeg!
### HTML5 Player
Menggunakan howler.js dan Clappr, alat audio dan video yang sederhana namun kuat. Mereka memanfaatkan kemampuan pemutar media browser Anda tanpa plugin pihak ketiga.
### Awesome Backbone
KooZic menggunakan versi ringan dari Odoo sebagai tulang punggung. Kami memanfaatkan kekuatan perangkat lunak untuk fokus pada satu tugas: mengembangkan perangkat lunak streaming musik dan video.

## Referensi
   1. [Tentang KooZic](https://github.com/DocMarty84/koozic) - DocMarty84
   2. [Instalasi Otomatis](https://koozic.net/installation/) - koozic.net
   3. [Instalasi Manual](https://doc.koozic.net/installation/detailed_instructions.html) - doc.koozic.net
   4. [Review KooZic](https://www.compsmag.com/alternative/software/koozic/) - compsmag.com
