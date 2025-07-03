# Analisis Sentimen Berita Keuangan dari CNN Lite

Skrip Python ini dirancang untuk melakukan *web scraping* artikel berita dari situs CNN Lite (`lite.cnn.com`), menganalisis sentimen dari paragraf pertama setiap berita, dan memvisualisasikan kata-kata yang paling sering muncul ke dalam sebuah *Word Cloud*. Analisis sentimen dilakukan menggunakan dua metode: **TextBlob** untuk analisis polaritas dan **Hugging Face Transformers** dengan model *finBERT* yang dikhususkan untuk teks keuangan.

## 📝 Deskripsi

Proyek ini mengotomatiskan proses pengumpulan dan analisis data berita dari CNN Lite. Prosesnya dimulai dengan mengambil 15 URL artikel dari halaman utama. Selanjutnya, skrip akan mengunjungi setiap URL untuk mengekstrak informasi detail seperti judul, penulis, tanggal terbit, dan konten paragraf pertama.

Setelah data terkumpul, dilakukan analisis sentimen ganda untuk mendapatkan wawasan yang lebih komprehensif:

1.  **TextBlob**: Memberikan skor kuantitatif untuk polaritas (negatif ke positif) dan subjektivitas (objektif ke subjektif).
2.  **Hugging Face Transformers (ProsusAI/finbert)**: Menggunakan model *finBERT* yang telah dilatih secara khusus pada data keuangan untuk mengklasifikasikan sentimen ke dalam kategori *Positive*, *Negative*, atau *Neutral* beserta skor keyakinannya.

Hasil akhir, termasuk data mentah dan skor sentimen dari kedua metode, disimpan dalam format CSV. Selain itu, sebuah *Word Cloud* dibuat untuk menyoroti kata-kata kunci yang paling dominan dari seluruh berita yang di-*scrape*.

## ✨ Fitur

  - **Web Scraping**: Mengambil daftar artikel dan konten detailnya dari CNN Lite.
  - **Analisis Sentimen Ganda**:
      - Menggunakan TextBlob untuk analisis polaritas/subjektivitas.
      - Menggunakan model *finBERT* dari Hugging Face untuk analisis sentimen di domain keuangan.
  - **Pemrosesan Data**: Mengelola dan menyimpan data yang telah diolah ke dalam struktur Pandas DataFrame.
  - **Ekspor Data**: Menyimpan hasil akhir ke dalam file `.csv`.
  - **Visualisasi Data**: Menghasilkan gambar *Word Cloud* untuk visualisasi frekuensi kata.

## 📚 Ketergantungan (Dependencies)

Untuk menjalankan skrip ini, Anda memerlukan *library* Python berikut. Anda dapat menginstalnya menggunakan pip:

```bash
pip install requests beautifulsoup4 pandas transformers textblob wordcloud matplotlib --quiet
```

## 🚀 Cara Menjalankan

1.  Pastikan semua *dependencies* di atas sudah terpasang.
2.  Jalankan sel-sel kode di dalam file `.ipynb` secara berurutan.
3.  Skrip akan secara otomatis:
      - Mengambil *link* berita dari halaman utama CNN Lite.
      - Melakukan *scraping* detail dari setiap *link* berita.
      - Menganalisis sentimen menggunakan TextBlob dan Transformers.
      - Menyimpan data akhir ke dalam file CSV.
      - Menghasilkan dan menampilkan *Word Cloud*.
4.  Jika dijalankan di lingkungan Google Colab, file CSV hasil akhir akan otomatis ditawarkan untuk diunduh.

## 🛠️ Penjelasan Kode

  - **Instalasi dan Impor**: Sel pertama dan kedua menginstal semua pustaka yang diperlukan dan mengimpornya ke dalam lingkungan kerja.
  - **Konfigurasi**: Mengatur variabel global untuk nama file output, seperti `CSV_FILE_NAME` dan `WORDCLOUD_FILE_NAME`, berdasarkan nomor NPM.
  - **Soal 1: Pengambilan Link Berita**: Skrip mengakses `https://lite.cnn.com` dan mengambil 15 URL artikel berita dari elemen `<li>` pada halaman tersebut untuk di-*scrape* lebih lanjut.
  - **Soal 2: Scraping Detail Berita**: Skrip melakukan iterasi pada setiap URL yang telah dikumpulkan untuk mengekstrak data detail, seperti **Judul, Penulis, Tanggal Terbit, Jam Terbit, Sumber Berita, Baris Pertama Berita**, dan **Link Berita Utuh**. Data ini disimpan dalam sebuah Pandas DataFrame dan juga file CSV sementara (`..._Limabelas(without sentiment).csv`).
  - **Soal 3: Analisis Sentimen**:
      - **TextBlob**: Menganalisis kolom "Baris Pertama Berita" untuk menghitung **polaritas** (rentang -1 hingga 1) dan **subjektivitas** (rentang 0 hingga 1). Hasilnya ditambahkan ke DataFrame sebagai kolom `polarity_textblob` dan `subjectivity_textblob`.
      - **Hugging Face**: Menggunakan *pipeline* `text-classification` dengan model `ProsusAI/finbert`. Model ini menganalisis "Baris Pertama Berita" dan menghasilkan label sentimen (`positive`, `negative`, `neutral`) dan skor keyakinan. Hasilnya ditambahkan sebagai kolom `HFLabel` dan `HFScores`.
  - **Soal 4: Pembuatan Word Cloud**: Menggabungkan semua teks dari kolom "Baris Pertama Berita" untuk membuat dan menampilkan visualisasi *Word Cloud*.
  - **Penyimpanan File Akhir**: Menyimpan DataFrame akhir yang sudah berisi analisis sentimen ke dalam file `240310220056_Limabelas.csv` dan gambar *Word Cloud* ke file `240310220056_WordCloud.png`.

## 📤 Output

Skrip ini akan menghasilkan dua file utama:

1.  **`240310220056_Limabelas.csv`**: Sebuah file CSV yang berisi data terstruktur dari artikel berita yang telah dianalisis.
2.  **`240310220056_WordCloud.png`**: Sebuah file gambar yang memvisualisasikan kata-kata yang paling umum dalam kumpulan data berita.

## 🧑‍💻 Author

  - **Nama**: Marsello Ormanda
  - **NPM**: 240310220056
