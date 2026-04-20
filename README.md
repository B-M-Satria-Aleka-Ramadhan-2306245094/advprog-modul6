## Reflection 1
Fungsi handle_connection berperan sebagai unit pemroses utama untuk setiap permintaan yang masuk melalui protokol TCP. Berikut adalah ringkasan teknis mengenai cara kerja metode tersebut:

Efisiensi Pembacaan Data
Penggunaan BufReader bertujuan untuk mengoptimalkan kinerja sistem. Alih-alih melakukan pembacaan data secara langsung dari TcpStream yang melibatkan banyak system call, BufReader menyimpan data ke dalam memori perantara (buffer) sehingga proses pembacaan menjadi lebih cepat dan efisien.

Transformasi Data dan Iterator
Data yang diterima diproses menggunakan rangkaian fungsi iterator untuk mendapatkan informasi yang relevan:

- Lines: Membagi aliran data mentah menjadi sekumpulan baris teks.

- Map: Melakukan ekstraksi nilai dari tipe data Result agar data teks bisa diolah lebih lanjut.

- Take While: Berfungsi sebagai pembatas logis. Sesuai standar HTTP, baris kosong menandakan akhir dari bagian header permintaan. Fungsi ini memastikan program berhenti membaca tepat pada batas tersebut.

- Collect: Menggabungkan hasil pemrosesan ke dalam sebuah Vector agar data tersimpan secara permanen di memori untuk kebutuhan analisis atau logging.

Visualisasi Output
Pencetakan hasil menggunakan format debug dalam println bertujuan untuk mempermudah pemeriksaan struktur data. Hal ini memastikan bahwa seluruh pesan yang dikirimkan oleh klien telah diterima secara utuh dan sesuai dengan format yang diharapkan sebelum server memberikan respon balik.

## Reflection 2
Pada tahap ini, fungsi handle_connection telah diperbarui sehingga tidak hanya membaca permintaan, tetapi juga memberikan respons balik. Program kini membaca file eksternal hello.html menggunakan modul fs (file system) dan mengirimkan isinya kembali ke klien melalui stream. 

Hal yang dipelajari adalah pentingnya mematuhi format protokol HTTP, yaitu menyertakan baris status, header (seperti Content-Length), dan pemisah baris kosong sebelum mengirimkan isi konten. Hal ini memungkinkan browser untuk mengenali dan menampilkan halaman HTML dengan benar.

![Commit 2 screen capture](assets/images/commit2.png)
