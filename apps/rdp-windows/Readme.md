# 💻 Windows 10 Multi-User RDP Server with RDPWrap

Dokumentasi ini menjelaskan cara mengonfigurasi Windows 10 (Home/Pro) agar bisa diakses oleh banyak user secara bersamaan (*concurrent sessions*) menggunakan **RDP Wrapper Library**.

## 📌 Deskripsi Proyek
Secara default, Windows 10 mematikan fitur multi-user RDP (menggunakan license). Dengan menggunakan RDP Wrapper Opensource, kita bisa memfungsikan Windows 10 layaknya Windows Server, sehingga beberapa user bisa login dan bekerja di desktop masing-masing secara simultan tanpa saling mengeluarkan (*kick*).

## 🛠️ Persiapan & Alat
* **Sistem Operasi:** Windows 10 (Pro disarankan, Home bisa namun terbatas).
* **Software:** [RDP Wrapper Library](https://github.com/stascorp/rdpwrap) (Gunakan versi terbaru).
* **Update Tool:** [RDPWInst](https://github.com/sebaxakerhtc/rdpwrap.ini) (Untuk memperbarui file `rdpwrap.ini` agar sesuai dengan build Windows terbaru).

---

## 🚀 Langkah Instalasi

### 1. Persiapan User
Buat beberapa user account di Windows 10 Anda:
1. Masuk ke **Settings > Accounts > Other Users**.
2. Tambahkan user baru (misal: `client01`, `client02`).
3. Pastikan setiap user memiliki password.

### 2. Instalasi RDP Wrapper
1. Download file ZIP RDP Wrapper dan ekstrak.
2. Klik kanan pada `install.bat` dan pilih **Run as Administrator**.
3. Tunggu hingga proses selesai.

### 3. Konfigurasi & Cek Status
Buka file `RDPConf.exe` untuk melihat status. 
* **Wrapper State:** Harus `Installed`.
* **Service State:** Harus `Running`.
* **Listener State:** Harus `Listening`.

### 4. Mengatasi "Listener State: Not Supported"
Jika muncul pesan *Not Supported*, artinya file `rdpwrap.ini` Anda tidak mengenali versi Windows Update Anda.
1. Download file `rdpwrap.ini` terbaru dari komunitas (seperti di repositori *sebaxakerhtc*).
2. Stop service RDP: Buka CMD (Admin) lalu ketik `net stop termservice`.
3. Copy file `.ini` terbaru ke folder `C:\Program Files\RDP Wrapper\`.
4. Jalankan kembali service: `net start termservice`.

---

## 🔒 Optimasi Keamanan & Akses
Agar server RDP Anda aman dan lancar di akses banyak orang:

1. **Ubah Port RDP Default:**
   Ubah port `3389` ke port lain melalui Registry Editor untuk menghindari serangan *brute force*.
2. **Pengaturan Firewall:**
   Pastikan port yang Anda pilih sudah di-izinkan (*Allow*) di Windows Firewall.
3. **Optimasi RAM:**
   Karena banyak user akan login, pastikan RAM fisik server Anda mencukupi (Minimal 8GB-16GB untuk 5-10 user ringan).
4. **Cloudflare WARP:**
   Gunakan konfigurasi WARP (lihat dokumentasi sebelah) agar IP publik Windows Anda tetap terproteksi.

---

## ⚠️ Peringatan (Disclaimer)
* **Windows Update:** Setiap kali Windows melakukan update besar, RDP Wrapper seringkali berhenti bekerja dan perlu di-update file `.ini` nya.
* **Lisensi:** Penggunaan RDP Wrapper pada Windows 10 mungkin melanggar *EULA* Microsoft untuk penggunaan komersial skala besar. Gunakan untuk tujuan edukasi dan lab pribadi.

---
**Author:** Agus Sulistiono - Zyfatech Labs  
**Project:** Ruang Cloud (Budget RDP Solutions)