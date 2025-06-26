Berikut analisis hasil BERTopic dengan `min_cluster_size=200`, diformat dalam `.md` siap copy:

---

# **Analisis Hasil BERTopic (`min_cluster_size=200`)**

## 📌 **Ringkasan Umum**

Dengan `min_cluster_size=200`, model menghasilkan **33 topik**. Dari segi kualitas:

* Struktur topik lebih ringkas dibanding versi 150
* Beberapa topik negatif tetap terdeteksi
* Masih terdapat topik tidak informatif (emoji-only, stopword)

---

## ✅ **Topik Relevan dan Informatif (Positif atau Netral Bermakna)**

| Topic | Keywords                                                | Catatan                                    |
| ----- | ------------------------------------------------------- | ------------------------------------------ |
| 1     | danantaraporosinvestasi, investasi, pemerintah, sinergi | Core tema proyek                           |
| 3     | prabowo, presiden, badan, nusantara, anagata, bpi       | Pemerintahan dan aktor                     |
| 5     | infrastruktur, danantarabangunnegeri, pembangunan       | Narasi pembangunan                         |
| 6     | terpercaya, digital, teknologi, digitalisasi, inovasi   | Isu transformasi digital                   |
| 8     | mendorong, pertumbuhan, strategis, aset                 | Tema ekonomi makro                         |
| 9     | gerakcepatekonomihebat, efisiensi, global, transparansi | BUMN & efektivitas                         |
| 11    | negara, aset, kekayaan, produktif                       | Ekonomi negara                             |
| 14    | berkelanjutan, bumn, optimalisasi, investasi            | Efisiensi sektor BUMN                      |
| 18    | buruhbersamaprabowo, inovasi, digital                   | Gerakan buruh & digitalisasi               |
| 22    | transparansi, anggaran, efisiensi                       | ***Bisa jadi kritik halus***               |
| 24    | optimisme, pertumbuhan, peresmian                       | Narasi positif proyek                      |
| 30    | sby, jokowi, pengawasan, aset                           | Campuran isu lintas rezim                  |
| 32    | hukum, landasan, dasar, kokoh                           | ***Kebijakan hukum, bisa netral-positif*** |

---

## ❗ **Topik Kritik / Isu Negatif**

| Topic | Keywords                                   | Indikasi                            |
| ----- | ------------------------------------------ | ----------------------------------- |
| 20    | indonesiagelap, ndasmu, pertamax, exabet88 | Satir, sindiran tajam               |
| 22    | transparansi, anggaran, efisiensi          | Kritik implisit soal pengelolaan    |
| 26    | polri, kolaborasi, mengawal, komitmen      | Berpotensi arah pro/kontra keamanan |
| 30    | pengawasan, amp, produktif                 | Bisa dimonitor untuk kritik publik  |

**➡️ Fokus eksplorasi lebih lanjut**: `topic 20, 22, 30`

---

## ⚠️ **Topik Ambigu / Tidak Informatif / Noise**

| Topic              | Keywords                                | Masalah                          |
| ------------------ | --------------------------------------- | -------------------------------- |
| 0                  | *(kosong)*                              | Bug atau topik kosong            |
| 16, 17, 19, 21, 27 | Hanya emoji/sentiment                   | Tidak bermakna tematik           |
| 28                 | harga, dm, size, varian                 | Kemungkinan spam atau e-commerce |
| 35                 | monkey, kalo                            | Tidak jelas konteksnya           |
| 31                 | rolling\_on\_the\_floor\_laughing, gini | Kurang bermakna                  |

---

## 🧹 **Rekomendasi Pembersihan**

1. **Hapus Topik Emoji/Sentiment-Only**
   Tambahkan pre-cleaning:

   ```python
   import re
   def clean_text(text):
       text = re.sub(r'[^\w\s,.!?]', '', text)  # Hapus emoji/simbol
       return ' '.join([w for w in text.lower().split() if w not in stopwords])
   ```

2. **Cek penyebab topic 0 kosong**
   Bisa jadi:

   * Tweet pendek berulang
   * Kesalahan tokenisasi
   * Kosakata tidak dikenali model

3. **Isolasi & Evaluasi Kritik**
   Ambil `df_topic` yang `topic` = 20, 22, 30 → lakukan evaluasi manual/visualisasi isi untuk konfirmasi nilai strategisnya.

---

## 📈 **Visualisasi Distribusi Topik**

Disarankan tetap plot distribusi topik untuk melihat proporsi dominasi:

```python
import matplotlib.pyplot as plt
df_topic['topic'].value_counts().plot(kind='bar', figsize=(12,6), title="Distribusi Tweet per Topik (min_cluster_size=200)")
plt.tight_layout()
plt.savefig("topic_distribution_200.png")
```

---

## ✅ **Kesimpulan**

* Setting `min_cluster_size=200` memberikan topik yang **lebih padat**, namun **masih mempertahankan sebagian tema kritik**.
* Masalah topik noise (emoji-only) masih muncul, namun sedikit lebih terkendali.
* Disarankan tetap lakukan:

  * Cleaning lebih agresif
  * Filtering berdasarkan topik untuk pendalaman (terutama topik kritik)
  * Kombinasi dengan **sentiment scoring** untuk validasi intensi

**Rekomendasi Lanjut:**
Jika ingin mengarah pada pemetaan opini publik (pro-kontra), ekstrak `topic 20, 22, 30`, lalu lakukan:

* Visualisasi isi tweet-nya
* Klasifikasi manual
* Clustering ulang (sub-BERTopic) dengan `min_cluster_size=20–50`

---
