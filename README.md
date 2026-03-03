# 🚚 JNE API Governance & Discovery Integration (Phase 2)

Proyek ini mendemonstrasikan otomatisasi **Tata Kelola (Governance)** dan **Penemuan (Discovery)** API JNE dengan mengintegrasikan GitHub ke **IBM API Connect**. Fokus utama fase ini adalah implementasi *Shift-Left Approach* untuk validasi desain sebelum publikasi.

## 🌟 Fitur Utama
* **Automated Linting**: Validasi otomatis file OpenAPI menggunakan **Spectral**.
* **Shift-Left Governance**: Menghentikan alur kerja (build) jika ditemukan pelanggaran standar desain.
* **Secure Integration**: Menggunakan **GitHub Secrets** (`apicApikey`) untuk koneksi aman ke IBM Cloud.
* **Centralized Discovery**: Sinkronisasi otomatis ke katalog **IBM API Manager**.

---

## 🛠️ Alur Kerja CI/CD
Sistem akan menjalankan urutan berikut setiap kali ada perubahan pada kode:
1.  **Checkout**: Mengambil kode terbaru dari repositori.
2.  **Linting (Spectral)**: Memeriksa kualitas desain API berdasarkan aturan `.spectral.yaml`.
3.  **Discovery (IBM APIC)**: Jika lolos validasi, file `openapi2.yaml` dikirim ke IBM API Connect.



---

## ⚠️ Limitasi Teknis (Sesuai Arahan Management)
Penting untuk memahami batasan sistem dalam fase ini:
* **Sumber Terverifikasi**: Discovery hanya didukung untuk **GitHub** dan **DataPower Gateway**.
* **Third-Party Gateways**: Sistem **tidak bisa** melakukan discovery otomatis langsung dari runtime **Kong** atau **Apigee**.
* **Metodologi**: API pada gateway eksternal wajib didaftarkan dokumennya di GitHub agar tetap masuk dalam pengawasan tata kelola pusat.

---

## 🧪 Simulasi Validasi (Demo)
Untuk menunjukkan fungsi **Breaking the Build**, demo dilakukan dengan:
1.  Memasukkan endpoint yang tidak sesuai (misal: `/get_data_jne` bukan `camelCase`).
2.  Menghapus parameter `security` (Autentikasi).
3.  **Hasil**: GitHub Actions akan berubah menjadi **Merah (Fail)** dan mencegah pengiriman data ke IBM API Connect sampai kesalahan diperbaiki.

---

## 📖 Cara Konfigurasi
1.  Simpan API Key di **Settings > Secrets > Actions** dengan nama `apicApikey`.
2.  Pastikan file `openapi2.yaml` berada di root folder.
3.  Push perubahan untuk memicu alur kerja otomatis.
