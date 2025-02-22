# Project15
## Langkah-langkah Performing Table Joins

1. Temukan file tl_2019_06_tract.zip di Browser QGIS dan kembangkan. Pilih file tl_2019_06_tract.shp dan seret ke kanvas.

2. Dialog Select Transformation akan meminta untuk mengkonversi dari EPSG:4269 ke EPSG:4326. Dialog ini menyajikan beberapa transformasi untuk mengkonversi antara koordinat antara proyeksi tersebut. Tinggalkan pilihan ke pilihan default dan klik OK.

3. Anda akan melihat layer tl_2019_06_tract dimuat di panel Layers. Lapisan ini berisi batas-batas bidang sensus di California. Klik kanan pada layer tl_2019_06_tract dan pilih Open Attribute Table.

4. Periksa atribut layer. Untuk menggabungkan tabel dengan lapisan ini, kita memerlukan atribut unik dan umum dari setiap fitur. Dalam hal ini, ada 8057 rekaman traktat individual dengan bidang GEOID. Kolom ini dapat menautkan lapisan ini dengan lapisan atau tabel lain yang berisi ID yang sama.

5. Untuk memuat data tabular, klik Open Data Source Manager.

6. Dalam dialog Pengelola Sumber Data, pilih Teks yang Dibatasi. Kemudian di sebelah kanan, klik ... di sebelah Nama file dan ramban ke folder yang tidak di-zip dengan CSV populasi California.

7. Sekarang di bawah Data Sampel, kita dapat memeriksa data bahkan sebelum memuatnya sebagai lapisan. Representasi menunjukkan bahwa tabel data berisi 2 baris header.

8. Untuk menghilangkan baris tajuk tambahan, di bawah Opsi Rekam dan Bidang atur Jumlah baris tajuk untuk dibuang ke 1. Sekarang tabel akan berisi tajuk kolom yang tepat. Karena lapisan ini hanya berisi data tabular, pilih Tanpa geometri (tabel hanya atribut) di bawah Definisi Geometri. Klik Add untuk menambahkannya sebagai layer dan kemudian klik Close untuk menutup kotak dialog ini.

9. CSV sekarang akan diimpor sebagai tabel ke QGIS dan muncul sebagai ACST5Y2019.S0101 di panel Lapisan. Sekarang klik kanan pada layer dan pilih Open Attribute Table.

10. Kolom ID berisi id unik untuk setiap record, yang dapat digunakan untuk menggabungkan tabel ini dengan layer tl_2019_06_tract. Jika Anda membandingkan nilai ID dengan kolom GEOID dari tl_2019_06_tract. Anda akan melihat bahwa itu diawali dengan 1400000US. Untuk menggabungkan kedua tabel ini dengan sukses, nilainya harus sama persis. Mari hapus awalan ini dan tambahkan kolom baru dengan 11 karakter terakhir yang berisi nilai yang sama persis.

11. Untuk membuat kolom baru dengan 11 digit terakhir, buka Processing Toolbox dengan masuk ke Processing ‣ Toolbox, dan cari dan temukan tabel Vector ‣ Algoritma kalkulator lapangan.

12. Dalam dialog Kalkulator bidang, pilih ACST5Y2019.S0101 sebagai lapisan Input, masukkan geoid di Nama bidang, dan pilih string di Jenis Bidang Hasil. Sekarang cari substr dalam ekspresi. Kita dapat menggunakan fungsi ini untuk mengekstrak bagian yang diperlukan dari kolom id.

13. Masukkan ekspresi di bawah ini. Kami menggunakan fungsi substr dan mengekstrak nilai dari posisi -11 (nilai negatif dihitung dari akhir). Hasil akhir dapat dilihat di bagian Pratinjau. Klik Jalankan.

14. Sekarang lapisan baru Dihitung akan dimuat di kanvas, mari kita periksa tabel atribut. Geoid kolom baru dengan nilai yang dapat disesuaikan dengan saluran sensus akan hadir.

15. Untuk membuat gabungan tabel, buka Processing Toolbox dengan masuk ke Processing ‣ Toolbox, dan cari dan temukan atribut Vector general ‣ Join dengan algoritma nilai bidang.

16. Dalam dialog Gabungkan atribut berdasarkan nilai bidang, pilih tl_2019_06_tract sebagai lapisan Input dan GEOID sebagai bidang Tabel. Pilih Dihitung sebagai Input layer 2 dan geoid sebagai kolom Tabel 2. Di bawah kolom Layer2 untuk menyalin, klik ....

17. Periksa Nama Area Geografis, Perkirakan!!Jumlah!!Jumlah penduduk dan geoid. Klik Oke.

18. Periksa catatan Buang yang tidak dapat digabungkan. Ini akan menghilangkan catatan tambahan apa pun di tabel populasi. Klik tombol … di bawah layer gabungan untuk memilih lokasi file output dan pilih Save to File....

19. Beri nama geopackage keluaran sebagai california_total_population.gpkg . Klik Jalankan.

20. Setelah pemrosesan selesai, verifikasi bahwa algoritme berhasil jika semua fitur 8057 digabungkan. Klik Tutup.

21. Anda akan melihat layer baru california_total_population dimuat di panel Layers. Pada titik ini, bidang dari file CSV digabungkan dengan lapisan saluran sensus. Sekarang setelah kita memiliki data kependudukan di lapisan sensus, kita dapat menatanya untuk membuat visualisasi distribusi kepadatan penduduk. Klik tombol Buka Panel Penataan Lapisan.

22. Di panel Layer Styling, pilih Graduated dari menu drop-down. Saat kami ingin membuat peta kepadatan populasi, kami ingin menetapkan warna berbeda untuk setiap fitur saluran sensus berdasarkan kepadatan populasi. Kami memiliki populasi di bidang Estimasi!!Total!!Total populasi, dan bidang area di ALAND. Klik tombol Ekspresi, untuk menghitung persentase jumlah penduduk pada setiap saluran pencacahan.

         Note :

Saat membuat peta tematik (choropleth) seperti ini, penting untuk menormalkan nilai yang Anda petakan. Memetakan jumlah total per poligon tidak benar. Penting untuk menormalkan nilai-nilai yang dibagi dengan luas. Jika Anda menampilkan total seperti kejahatan, Anda dapat menormalkannya dengan membaginya dengan total populasi, sehingga memetakan tingkat kejahatan dan bukan kejahatan. Belajarlah lagi

23. Masukkan ekspresi berikut untuk menghitung kepadatan populasi. Area fitur diberikan dalam kilometer persegi. Kami kemudian mengubahnya menjadi meter persegi dengan mengalikannya dengan 1000000 dan menghitung kepadatan penduduk dengan rumus Penduduk/Luas. Pratinjau hasilnya dan klik OK.

24. Di Panel Penataan Lapisan, klik klasifikasikan dan masukkan kelas sebagai 10.

25. Klik pada jalur warna untuk memilih jalur warna RdYlGn.

26. Kerapatan yang lebih tinggi lebih penting, mari kita tetapkan warna hijau untuk kerapatan rendah dan merah untuk area dengan kerapatan tinggi. Klik pada jalur warna dan pilih Balikkan Jalur Warna.

27. Sekarang kami memiliki visualisasi informasi kepadatan populasi yang sangat baik di California. Untuk membuatnya lebih baik, mari kita buat batas setiap saluran sensus transparan. Klik pada tab Simbol.

28. Klik pada warna Stroke dan klik Stroke transparan.

29. Tempat sampah dapat disesuaikan, klik pada Nilai ini akan memunculkan dialog untuk memasukkan nilai batas atas dan bawah.

30. Setelah Anda puas menutup panel styling Layer. Kami sekarang memiliki visualisasi informasi kepadatan populasi yang terlihat bagus di California.

