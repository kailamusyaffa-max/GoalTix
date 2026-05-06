Nama Kelompok:
Dimas Ramadhan
Ghibran Rajendra
Kaila Musyaffa



 ⚙️ Database Trigger Documentation

Dokumentasi ini berisi daftar trigger yang digunakan dalam sistem **Tiket Pertandingan & Pembayaran** untuk menjaga konsistensi dan otomatisasi data.

---

🎟️ 1. Update Status Kursi

**Event:** `AFTER INSERT ON detail_transaksi`
**Tujuan:**
Menandai kursi sebagai terisi saat dipesan.

**Aksi:**

* Ubah `status` kursi menjadi `"Terisi"`

---

## 🗑️ 2. Kembalikan Status Kursi

**Event:** `AFTER DELETE ON detail_transaksi`
**Tujuan:**
Mengembalikan status kursi jika transaksi dibatalkan.

**Aksi:**

* Ubah `status` kursi menjadi `"Kosong"`

---

## 💰 3. Hitung Total Bayar

**Event:**

* `AFTER INSERT ON detail_transaksi`
* `AFTER UPDATE ON detail_transaksi`
* `AFTER DELETE ON detail_transaksi`

**Tujuan:**
Menghitung total pembayaran secara otomatis.

**Aksi:**

* Menjumlahkan seluruh `harga` dari detail transaksi

---

## 💳 4. Hitung Kembalian

**Event:** `AFTER INSERT ON pembayaran`
**Tujuan:**
Menghitung kembalian dari pembayaran.

**Rumus:**

```sql
kembalian = uang_bayar - total_bayar
```

---

## ✅ 5. Update Status Pembayaran

**Event:** `AFTER INSERT ON pembayaran`
**Tujuan:**
Menandai transaksi sebagai sudah dibayar.

**Aksi:**

* Set `status_bayar = "Lunas"`

---

## 🚫 6. Cegah Double Booking Kursi

**Event:** `BEFORE INSERT ON detail_transaksi`
**Tujuan:**
Mencegah kursi yang sama dipesan lebih dari sekali.

**Logika:**

* Cek status kursi
* Jika sudah `"Terisi"` → batalkan insert

---

## ⚠️ 7. Validasi Pembayaran

**Event:** `BEFORE INSERT ON pembayaran`
**Tujuan:**
Memastikan uang yang dibayar mencukupi.




 Ringkasan Trigger

No  Trigger                  Fungsi               
    
 1   Detail Transaksi Insert  Update kursi         
 2   Detail Transaksi Delete  Kembalikan kursi     
 3   Detail Transaksi (All)   Hitung total bayar   
 4   Pembayaran Insert        Hitung kembalian     
 5   Pembayaran Insert        Update status bayar  
 6   Detail Transaksi Insert  Cegah double booking 
 7   Pembayaran Insert         Validasi pembayaran  

 <img width="1356" height="1600" alt="image" src="https://github.com/user-attachments/assets/c9a6feb1-9a26-4073-b40d-2912504cbe04" />





