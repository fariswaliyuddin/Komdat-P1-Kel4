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
    
## Cara Pemakaian

## Pembahasan
### Free & Open-Source
### Search Thanks to ID3 Tags
### Enjoy Powerful Playlists
### Any music or video format
### HTML5 Player
### Awesome Backbone

## Referensi
    [Tentang KooZic](https://github.com/DocMarty84/koozic) - DocMarty84
    [Instalasi Otomatis](https://koozic.net/installation/) - koozic.net
    [Instalasi Manual](https://doc.koozic.net/installation/detailed_instructions.html) - doc.koozic.net
    [Review KooZic](https://www.compsmag.com/alternative/software/koozic/) - compsmag.com
