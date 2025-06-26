# **Analisis Hasil BERTopic (min\_cluster\_size=150)**

## 📌 **Ringkasan Umum**

Dengan setting `min_cluster_size=150`, model berhasil mendeteksi **44 topik**. Dibanding konfigurasi sebelumnya (`min_cluster_size=300`), hasil ini:

* Lebih beragam dalam tema
* Mulai menangkap topik negatif dan kritik secara lebih eksplisit
* Namun masih menyisakan beberapa topik tidak informatif (emoji-only, filler)

---

## ✅ **Topik Relevan dan Informatif (Positif atau Netral Bermakna)**

| Topic | Keywords                                                         | Catatan                            |
| ----- | ---------------------------------------------------------------- | ---------------------------------- |
| 1     | danantaraporosinvestasi, investasi, pemerintah, sinergi, langkah | Umum namun relevan                 |
| 4     | prabowo, presiden, badan, anagata, nusantara                     | Fokus pada aktor politik           |
| 5     | infrastruktur, danantarabangunnegeri, pembangunan                | Tema pembangunan                   |
| 7     | terpercaya, digital, danantarabangunnegeri, teknologi            | Transformasi digital               |
| 9     | gerakcepatekonomihebat, efisiensi, bumn                          | Narasi efisiensi dan modernisasi   |
| 10    | negara, aset, terpercaya, produktif                              | Isu ekonomi makro                  |
| 11    | kota, dukungan, masyarakat, semangat                             | Citra dukungan publik              |
| 14    | berkelanjutan, optimalisasi, bumn                                | Sektor BUMN                        |
| 18    | doa, harapan, kemajuan                                           | Tema religius dan aspiratif        |
| 20    | buruhbersamaprabowo, inovasi, digital                            | Gerakan buruh pro-rezim            |
| 25    | transparansi, anggaran, efisiensi                                | Cenderung kritik halus             |
| 31    | sby, jokowi, pengawasan, produktif                               | Campuran lintas era pemerintahan   |
| 42    | presidenprabowo, berita, diaudit, transparansi                   | Potensi isu audit dan transparansi |

---

## ⚠️ **Topik Ambigu / Noise / Tidak Informatif**

| Topic                  | Keywords                               | Masalah                                     |
| ---------------------- | -------------------------------------- | ------------------------------------------- |
| 0                      | *(kosong)*                             | Tidak ada keywords                          |
| 26, 33, 15, 21, 24, 28 | Hanya emoji                            | Tidak mengandung informasi tematik          |
| 30                     | harga, dm, bahan, size, varian, renang | Kemungkinan spam/off-topic                  |
| 32                     | the, is, to, this, of, it, you         | Bahasa Inggris stopword—*bug di tokenizer?* |
| 3                      | rakyat                                 | Terlalu umum                                |
| 43                     | money, monkey, face                    | Noise + emoji campuran                      |

---

## ❗ **Topik Kritik / Isu Negatif yang Layak Ditindaklanjuti**

| Topic | Keywords                                   | Indikasi                         |
| ----- | ------------------------------------------ | -------------------------------- |
| 23    | indonesiagelap, ndasmu, pertamax, exabet88 | Kritik, sindiran, satir          |
| 34    | indonesiagelap2025, hambalang, mangkrak    | Kritik pembangunan & IKN         |
| 36    | korupsi, koruptor, bancakan, sarang        | Isu korupsi – ***target utama*** |
| 25    | transparansi, anggaran, efisiensi          | Kritik birokrasi?                |
| 42    | diaudit, transparansi, akuntabilitas       | Muncul lagi – penting            |
| 23    | kaburajadulu, hutangnya                    | Kritik utang & distrust          |

**➡️ Rekomendasi:** Fokuskan eksplorasi ke topik 23, 34, 36, dan 42.

---

## 🛠️ **Rekomendasi Lanjutan**

1. **Bersihkan Stopword & Emoji**
   Topik emoji-only & stopword-only mengganggu. Perlu:

   * Regex untuk hapus emoji
   * Filter kata kosong umum (“aja”, “ya”, “gak”, dst)

2. **Periksa Tokenisasi Bahasa Inggris**
   Topic 32 hanya berisi kata dasar bahasa Inggris → bisa jadi bug tokenisasi dari `indobertweet`, karena tweet bercampur bahasa.

3. **Sentiment Analysis Post-processing** *(Opsional tapi kuat)*
   Tambahkan label sentimen di setiap tweet menggunakan model seperti `w11wo/indobertweet-base-sentiment` untuk:

   * Mengkategorikan topik sebagai *positive/neutral/negative*
   * Menvalidasi apakah topik tertentu memang dominan negatif

4. **Re-model khusus Topik Negatif**
   Ekstrak tweet dari topik 23, 34, 36, 42 → jalankan ulang BERTopic dengan `min_cluster_size=20` untuk menangkap subkritik atau variasi retorika.

---

## 📈 Distribusi Topik (Disarankan)

Untuk melengkapi analisis, tampilkan distribusi ukuran tiap topik:

```python
import matplotlib.pyplot as plt
df_topic['topic'].value_counts().plot(kind='bar', figsize=(12,6), title="Distribusi Tweet per Topik")
plt.tight_layout()
plt.savefig("topic_distribution_150.png")
```

---

## ✅ Kesimpulan

Tuning `min_cluster_size=150` **jauh lebih baik**:

* Topik lebih banyak dan variatif
* Topik kritik **mulai muncul secara signifikan**
* Tapi masih perlu pembersihan untuk menghilangkan noise, emoji, dan topik kosong

Langkah selanjutnya adalah **eksplorasi lanjutan pada topik negatif**, serta optimalisasi *data cleaning* sebelum embedding.

---
