# Laporan Analisis Topik Hasil BERTopic (`min_cluster_size=100`)

## 1. Ringkasan Umum

Pemodelan topik ini dilakukan pada data media sosial dengan menggunakan algoritma BERTopic dan parameter `min_cluster_size=100`. Hasil akhir menghasilkan total **56 topik**, dengan keragaman tema yang cukup luas, mencakup narasi resmi, sindiran politik, kritik sosial, kampanye digital, hingga kategori netral dan tidak bermakna (noise).

## 2. Temuan Utama

### A. Topik Narasi Resmi Pemerintah dan Program Korporat

Beberapa topik merepresentasikan narasi positif atau resmi terkait program-program investasi dan pembangunan:

* **Topik 1**: "danantaraporosinvestasi, investasi, pemerintah, sinergi, langkah"
* **Topik 4**: "infrastruktur, danantarabangunnegeri, pembangunan"
* **Topik 13**: "mendorong, pertumbuhan, strategis, investasi"
* **Topik 19**: "transparansi, anggaran, efisiensi, efisien, transparan, investasi"
* **Topik 34**: "fondasi, danantarabangunnegeri, kuat, membangun, kokoh, terpercaya"
* **Topik 8**: "gerakcepatekonomihebat, transformasi, efisien, global, bumn"

Topik-topik ini cenderung ditujukan untuk membangun kepercayaan publik terhadap institusi seperti Danantara dan BUMN.

### B. Topik Kritik, Satir, dan Sentimen Negatif

Terdapat beberapa topik dengan indikator kritik politik, sentimen negatif, hingga sarkasme:

* **Topik 17**: "indonesiagelap, ndasmu, malam, pertamax, exabet88, kaburajadulu" → sindiran, potensi anti-narasi.
* **Topik 41**: "indonesiagelap, 2029, adilijokowi, koruptor, napi" → konten bersifat politis dan keras.
* **Topik 47**: "hambalang, mangkrak, ikn, food, estate" → isu proyek gagal dan kritik terhadap pembangunan.
* **Topik 39 & 51**: kombinasi kata-kata sarkastik dan emoji, kemungkinan digunakan untuk menyindir atau mengejek.

Topik ini menandakan bahwa narasi kontra-naratif terhadap pembangunan dan tokoh tertentu tetap hidup dan signifikan.

### C. Topik Netral, Emosional, atau Noise

Beberapa topik terindikasi sebagai hasil dari ekspresi emosi, tidak terstruktur, atau tidak memiliki makna substansial:

* **Topik 18**, **32**, **40**, **15**, **25**, **27**: emoji, reaksi, dan frasa humor.
* **Topik 24**: "light\_skin\_tone, middle\_finger, head\_shaking" → kemungkinan hasil noise dari ekspresi personal.
* **Topik 0**: kosong, harus dibuang pada tahap evaluasi lanjutan.

Topik-topik ini perlu difilter untuk analisis serius, meskipun bisa digunakan untuk mengukur engagement atau dinamika emosi publik.

### D. Topik Digitalisasi, Teknologi, dan Ekonomi

* **Topik 6**: "terpercaya, digital, danantarabangunnegeri, inovasi"
* **Topik 14**: "buruhbersamaprabowo, danantarabangunnegeri, digital"
* **Topik 50**: "sistem, terpercaya, sustain, investasi"
* **Topik 49**: "energi, transisi, hijau, bersih, mantap, angin"

Topik-topik ini menunjukkan bahwa narasi pembangunan berbasis teknologi dan ekonomi hijau cukup menonjol.

### E. Topik yang Bersifat Kampanye Politik atau Pencitraan Tokoh

* **Topik 3 dan 29**: terkait "prabowo", "presiden", "bpi", "roson"
* **Topik 33**: "tepatsolutifindonesia, prabowo, diaudit, transparan"
* **Topik 30**: "sby, jokowi, terpercaya, pengawasan"

Topik ini mendukung hipotesis bahwa percakapan publik banyak melibatkan citra tokoh politik dan trust-building.

## 3. Evaluasi Kualitas Topik

| Kategori                | Jumlah Topik | Catatan                                                               |
| ----------------------- | ------------ | --------------------------------------------------------------------- |
| Narasi pemerintah/resmi | 10+          | Terstruktur, konsisten, cenderung repetitif                           |
| Kritik/sindiran/negatif | 5–6          | Lebih tersembunyi, namun cukup eksplisit di beberapa topik            |
| Kampanye politik        | 3–4          | Konsisten muncul untuk figur Prabowo, Jokowi, dan narasi pembangunan  |
| Netral / Noise / Emoji  | >10          | Perlu pemfilteran, namun tetap informatif untuk studi persepsi publik |
| Kosong / tidak relevan  | 1–2          | Perlu dieliminasi secara manual                                       |

## 4. Rekomendasi Lanjutan

1. **Filter Topik Tidak Bermakna**:

   * Topik 0, 24, 31 sebaiknya dikeluarkan atau ditandai sebagai non-analisabel.

2. **Sentiment Analysis Topikal**:

   * Lakukan klasifikasi sentimen per topik untuk mengetahui apakah topik tersebut positif, negatif, atau netral.

3. **Fokus pada Topik Kritik**:

   * Lakukan analisis manual pada Topik 17, 41, 47 sebagai representasi kritik sosial-politik paling signifikan.

4. **Visualisasi Narasi**:

   * Gunakan *topic-word cloud* atau *intertopic distance map* untuk menggambarkan distribusi narasi.

5. **Komparasi dengan Topik Hasil min\_cluster\_size Berbeda**:

   * Bandingkan hasil ini dengan cluster size 150 dan 200 untuk melihat konsistensi kritik dan dominasi narasi.

## 5. Kesimpulan

Hasil BERTopic dengan `min_cluster_size=100` menghasilkan granularitas topik yang tinggi. Hal ini memungkinkan pemetaan narasi yang lebih spesifik dan deteksi kritik yang lebih jelas. Meskipun terdapat topik-topik noise dan emoji, distribusi topik cukup representatif terhadap dinamika percakapan publik yang bersifat politis, promosi pemerintah, serta kritik terhadap proyek besar. Namun, proses interpretasi tetap memerlukan validasi manual untuk memastikan bahwa tiap topik benar-benar sesuai konteks.

Penggunaan parameter ini direkomendasikan untuk eksplorasi awal serta deteksi isu dan kontra-narasi dalam data publik.
