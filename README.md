expand-ro
expand partisi root pada raspberry yang di install centos 7

### Untuk expand partisi root cukup menjalankan perintah
rootfs-expand

### sebelumnya akan saya jelaskan cara install centos 7 di raspberry pi 3 dan expand secara manual
### kenapa manual? karena saya ingin berbagi penderitaan dengan yang lain :D
### ini alternatif apabila tidak bisa menggunakan tool yang sudah di sediakan dari linux
### spesifikasi yang saya pakai :
### - Windows 7 32 bit
### - raspberry 3
### - sdcard 16 Gb
### yang di perlukan :
### 1. file etcher ==> liat file link.txt
### 2. iso centos 7 arm ==> liat file link.txt
### 3. card reader

###################     INSTALL RASPBERRY DI SD CARD    #############################################
### Langkah-langkahnya sebagai berikut :
### 1. ekstrak file CentOS-Userland-7-armv7hl-generic-Minimal-1804-sda.raw.xz yang menghasilkan file raw
### 2. menggunakan aplikasi etcher.io 
###    select image browse lokasi file CentOS-Userland-7-armv7hl-generic-Minimal-1804-sda.raw
### 3. select drive yang akan di gunakan sebagai media penyimpanan raspberry
### 4. klik flash dan tunggu hingga selesai
### 5. selesai anda sudah mempunyai OS centos di raspberry pi 3

###################     EXPAND PARTISI ROOT CENTOS 7 DI RASPBERRY PI    ###############################
### Langkah-langkahnya sebagai berikut :
### CARA CEPAT / UNTUK CENTOS 7.5.1804 ################################################################
### 1. login ke raspberry, default usernya root password centos
###    bisa di rubah dengan menggunakan passwd root
### 2. jalankan rootfs-expand
### 3. selesai

### CARA MANUAL  ######################################################################################
### Apabila tool yang tidak di sediakan tidak ada (meskipun 90% ada tergantung versi yang di install) bisa 
### menggunakan manual sebagai berikut :
### 1. untuk melihat sector partisi menggunakan perintah parted
###    parted
###    (parted)unit chs
###    (parted)print
### 2. login ke raspberry, default usernya root password centos
### 3. cek partisi yang ada dengan perintah df -h
### 4. cek penggunaan partisi yang menggunakan memori card ll /dev/mm*
### 5. untuk pengecekan jenis partisi jalankan perintah berikut fdisk /dev/mmcblk0
###    seharusnya akan terlihat 3 jenis partisi :
###    - 1. FAT32
###    - 2. Linux
###    - 3. Linux Swap
###   sebagai catatan partisi yang akan kita hapus adalah partisi ke 2
### 6. tekan tombol/huruf d untuk menghapus partisi
###    menghapus partisi bukan berrarti menghapus data, tetapi menghapus formatnya yang kemudian akan 
###    di kembalikan jika terdapat porsi yang mencukupi
### 7. sekarang seharusnya sudah bisa expand partis root
###    tekan tombol/huruf n untuk membuat partisi baru
### 8. akan di tampilkan inputan untuk memasukkan sector pertama dari partisi, secara default pilihan 
###    dimulai dari nilai partisi yang kosong -->tekan enter
### 9. akan di tampilkan inputan untuk memasukkan batas sector dari partisi, secara default berisi 
###    nilai partisi akhir -->tekan enter
### 10. kemudian simpan dengan tekan tombol/huruf w
### 11. kemudian restart sudo reboot
### 12. setelah sistem up dapat di cek kembali partisi yang sudah kita rubah df -h
###     seharusnya partisi masih belum berubah karena kita belum expand semua karena tadi konfigurasi masih tersimpan di ram
### 13. lakukan expand dan pemindahan data ke partisi yang baru (partisi root yang akan di expand dalam hal ini mmcblk0p4)
###     resize2fs /dev/mmcblk0p4
### 14. dan yang terakhir restart sudo reboot
### 15. cek ulang partisi df -h voila partisi sudah terexpand sesuai kapasitas yang ada



