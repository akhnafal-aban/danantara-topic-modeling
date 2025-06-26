# Analisis Tematik Mendalam untuk clustering terbaik (Clustering Size = 100)

## 1. **Gambaran Umum Distribusi Topik**

Model dengan `min_cluster_size=100` menghasilkan 56 topik. Distribusinya mencerminkan:

* **Topik positif/resmi** seperti pembangunan, optimisme, digitalisasi, investasi, dan dukungan terhadap pemerintah.
* **Topik informal/netral** seperti ekspresi emoji dan komentar santai.
* **Topik kritik dan sindiran** yang muncul eksplisit di beberapa klaster.

### Ringkasan Topik Berdasarkan Fungsi:

| Kategori Topik      | Contoh Topik                    | Karakteristik                                                      |
| ------------------- | ------------------------------- | ------------------------------------------------------------------ |
| **Resmi/Positif**   | `3`, `1`, `4`, `13`, `34`, `19` | Narasi pembangunan, optimisme, dan penguatan branding institusi    |
| **Informal/Netral** | `15`, `24`, `27`, `39`, `51`    | Dominasi emoji, humor, atau ekspresi tidak substantif              |
| **Kritik/Sindiran** | `17`, `41`, `47`                | Kritik terhadap proyek negara, sindiran terhadap narasi pemerintah |
| **Ambigu/Campuran** | `0`, `31`, `32`                 | Noise, topik tidak fokus, atau terlalu luas                        |

---

## 2. **Identifikasi Topik Kritik/Negatif**

| Topic  | Keywords                                                                         | Indikasi                                                                                            |
| ------ | -------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **17** | `indonesiagelap, ndasmu, malam, pertamax, exabet88, carmen, senin, kaburajadulu` | Kritik sarkastik terhadap kondisi nasional, menyisipkan istilah seperti *ndasmu* dan *kaburajadulu* |
| **41** | `indonesiagelap, 2029, adilijokowi, koruptor, pilpres, napi`                     | Kritik terhadap isu korupsi, ketimpangan, dan pemilu                                                |
| **47** | `hambalang, ikn, indonesiagelap2025, mangkrak`                                   | Mengarah ke kritik terhadap proyek nasional mangkrak dan sindiran IKN                               |
| **51** | `face_with_tears_of_joy, chart_increasing, gorilla, face_with_symbols_on_mouth`  | Kritik dengan pendekatan humor (meme) terhadap fenomena ekonomi atau sosial                         |
| **39** | `ngurus, cat_with_tears_of_joy`                                                  | Kritik tidak langsung terhadap pengelolaan, menggunakan nada sarkastik                              |

---

# Evaluasi Lanjutan: Strategi Perluasan dan Pembenahan Topik Kritik

## A. **Rekomendasi Teknis untuk Pemodelan Ulang**

1. **Gunakan Subset Filtering untuk Topik Kritik**

   * Buat subset data yang hanya berisi dokumen dari topik `17`, `41`, `47`, `39`, dan `51`.
   * Lakukan *reclustering* pada subset ini dengan `min_cluster_size` lebih kecil (misal 20–30) untuk memecah subtema seperti korupsi vs proyek mangkrak vs satire publik.

2. **Integrasikan Analisis Sentimen Per-Topik**

   * Tambahkan pipeline *sentiment classifier* (misalnya IndoBERT atau RoBERTa Indo).
   * Buat distribusi sentimen untuk setiap topik untuk membedakan topik:

     * Kritik emosional negatif
     * Kritik sarkastik
     * Humor sosial
     * Komplain netral

3. **Gunakan Representasi Konteks Semantik (Sentence Transformer)**

   * Lakukan embedding ulang menggunakan SBERT Indo (misal `indobert-base-p2`) untuk menilai *semantic proximity* antar-topik.
   * Tujuannya adalah untuk menemukan topik yang “berbeda keyword tapi sama makna”, misalnya:

     * `indonesiagelap` dan `kaburajadulu`
     * `koruptor` dan `mangkrak`

4. **Pemetaan Temporal (Jika Ada Data Waktu)**

   * Jika data memiliki informasi waktu, plot kemunculan topik `17`, `41`, `47` secara time series.
   * Bisa digunakan untuk menghubungkan kritik dengan kejadian aktual (misal debat capres, peluncuran proyek IKN).

---

## B. **Rekomendasi Strategis: Ekspansi dan Validasi Kritik**

1. **Cross-Matching dengan Media Berita**

   * Ambil topik/topik frasa seperti `hambalang`, `IKN`, `2029`, `koruptor`, lalu lakukan pencocokan silang dengan judul/headline media nasional.
   * Validasi apakah topik ini selaras dengan diskursus aktual.

2. **Kategorisasi Manual Topik Kritis**

   * Buat klasifikasi manual:

     * *Proyek mangkrak*
     * *Sindiran kebijakan*
     * *Kritik terhadap elite*
     * *Meme sindiran sosial*
   * Gunakan hasil klasifikasi ini untuk pelabelan supervised ke depannya.

3. **Evaluasi Konsistensi Kritik di Dataset Lain**

   * Bandingkan hasil clustering ini dengan korpus berbeda (misal Twitter publik tentang topik serupa) untuk memeriksa apakah topik kritik ini *unik* untuk dataset atau *umum* di masyarakat.

---

## C. **Indikator Awal Validasi Keberhasilan Topik Kritik**

| Indikator                                             | Syarat                                       |
| ----------------------------------------------------- | -------------------------------------------- |
| Distribusi sentimen negatif dominan di topik tertentu | ≥ 70% dari dokumen bernada negatif           |
| Koherensi topik tinggi (Coherence ≥ 0.4)              | Topik kritik harus konsisten secara leksikal |
| Topik kritik muncul kembali pada data berbeda         | Konsistensi across-corpus                    |
| Muncul hubungan dengan peristiwa aktual               | Cross-temporal evidence                      |

---

## Kesimpulan

Topik-topik kritik dalam hasil clustering ini menunjukkan indikasi awal bahwa publik tidak hanya menyerap narasi pembangunan yang positif, namun juga mengekspresikan kekecewaan atau sinisme terhadap proyek dan elite negara. Namun, untuk menyimpulkan makna mendalam dan konsistensi kritik tersebut, diperlukan langkah analitik lanjutan sebagaimana disarankan di atas.

Jika Naf menginginkan, saya dapat bantu mengembangkan pipeline filtering topik-topik negatif ini ke tahap visualisasi interaktif atau klasifikasi berbasis supervised learning.
