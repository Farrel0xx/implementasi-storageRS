# 🚀 SFTP Server untuk BPJS & Rumah Sakit
![Diagram SFTP BPJS](storage1.webp)

## 📌 Kenapa SFTP? 
Sistem saat ini (OneDrive) **tidak aman & tidak fleksibel**:
✅ **Data bisa diakses semua orang** → Rawan kebocoran data  
✅ **Tidak bisa hapus file** → Kesalahan input sulit diperbaiki  
✅ **Harus buat folder manual tiap hari** → Buang waktu  

**Solusi:** Pakai **SFTP (Secure File Transfer Protocol)** untuk sistem yang lebih aman, cepat, dan fleksibel!  

---

## 🛠️ 1. Setup SFTP Server (Untuk BPJS)

### 🔹 Install & Konfigurasi SFTP di Linux  
```bash
# Update & install OpenSSH Server
sudo apt update && sudo apt install openssh-server -y

# Buat user khusus untuk rumah sakit
sudo adduser rumahsakit
sudo passwd rumahsakit

# Buat folder penyimpanan data
sudo mkdir -p /sftp/rumahsakit
sudo chown root:root /sftp
sudo chown rumahsakit:rumahsakit /sftp/rumahsakit

# Batasi akses hanya ke SFTP (tidak bisa login SSH)
echo "Match User rumahsakit
    ChrootDirectory /sftp
    ForceCommand internal-sftp
    X11Forwarding no
    AllowTcpForwarding no" | sudo tee -a /etc/ssh/sshd_config

# Restart SSH service
sudo systemctl restart sshd
```

✅ **Sekarang server BPJS sudah siap menerima file dari rumah sakit!**  

---

## 📂 2. Akses SFTP dari Windows (Untuk Rumah Sakit)

### 🔹 Cara Akses dengan WinSCP / FileZilla  
1️⃣ **Download WinSCP** → [https://winscp.net](https://winscp.net)  
2️⃣ Masukkan **detail server SFTP**:  
   - **Host:** `IP-Kali-Linux`
   - **Port:** `22`
   - **Username:** `rumahsakit`
   - **Password:** `[password yang tadi dibuat]`
3️⃣ **Klik Login** → Langsung masuk ke folder `/sftp/rumahsakit`
4️⃣ **Drag & Drop file laporan rumah sakit ke dalam server!**  

✅ **File langsung tersimpan di server BPJS dengan aman & bisa dihapus/edit kalau ada kesalahan.**  

---

## 🔥 3. Test Upload & Download File

### 🔹 Dari Windows (WinSCP/FileZilla)  
- **Upload file ke server BPJS**  
- **Download file dari server BPJS ke Windows**  

### 🔹 Dari Terminal di Kali Linux  
```bash
# Login ke SFTP
sftp rumahsakit@IP-Kali-Linux

# Upload file
put laporan_klaim.pdf

# Download file dari server ke lokal
get data_claim_01.xlsx

# Keluar
exit
```

✅ **Sekarang rumah sakit bisa kirim & ambil data BPJS dengan mudah!**  

---

## 🚀 4. Demo di Depan BPJS / HealthHackathon

### **Keunggulan SFTP yang Bisa Ditunjukkan**:
✔ **Bisa upload file besar (ber-Giga-Giga) tanpa batas!**  
✔ **Data lebih aman dibanding OneDrive (terenkripsi SSH).**  
✔ **Rumah sakit bisa hapus & edit file kalau perlu revisi.**  
✔ **BPJS bisa ambil data otomatis tanpa ribet tracking manual.**  
✔ **Bisa buat folder harian otomatis, gak perlu bikin manual.**  

✅ **SFTP = Solusi terbaik buat BPJS & Rumah Sakit!**  

---

## 🔒 5. Next Step: Implementasi di BPJS  
1️⃣ **Coba setup di Kali Linux & tes upload dari WinSCP/FileZilla.**  
2️⃣ **Siapkan presentasi/demo untuk HealthHackathon atau BPJS.**  
3️⃣ **Dorong BPJS untuk upgrade sistem ke SFTP agar lebih aman & efisien.**  

📌 **Kalau ada kendala atau error, tinggal tanya! 🚀🔥**  
