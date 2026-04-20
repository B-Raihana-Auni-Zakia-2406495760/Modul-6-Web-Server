# Commit 1 Reflection notes
Pada tahap ini, saya mempelajari cara Rust menangani koneksi TCP sederhana dengan TcpListener yang di bind ke 127.0.0.1:7878 untuk menerima koneksi masuk. Setiap koneksi diproses lewat listener.incoming() dan ditangani oleh handle_connection. Data HTTP request dibaca menggunakan BufReader secara efisien, lalu dikumpulkan ke dalam vector agar mudah dipahami.

![Commit 2 screen capture](/assets/images/commit2.png)
# Commit 2 Reflection notes
Pada tahap ini, web server sudah bisa mengirim file HTML, bukan hanya mencetak request. File hello.html dibaca dengan fs::read_to_string, lalu dikirim sebagai response lengkap dengan HTTP/1.1 200 OK dan Content-Length. Semua digabung dengan format! dan dikirim ke stream agar bisa ditampilkan di browser.

![Commit 3 screen capture](/assets/images/commit3.png)
# Commit 3 Reflection notes
Server sekarang bisa memvalidasi request line dan memberi respons berbeda. Jika GET /, server mengembalikan hello.html dengan 200 OK. Jika path tidak dikenali (misalnya /bad), server mengirim 404 NOT FOUND dengan halaman 404.html.

# Commit 4 Reflection notes
Pada tahap ini terlihat keterbatasan server single-threaded. Saat rute /sleep dijalankan (delay 10 detik), server menjadi terblokir dan tidak bisa melayani request lain. Ini menunjukkan bahwa arsitektur ini tidak scalable dan perlu konkurensi agar request lambat tidak menghambat yang lain.

# Commit 5 Reflection notes
Server ditingkatkan menjadi multithreaded dengan ThreadPool berisi 4 worker agar lebih efisien. Pekerjaan dibagikan lewat channel (mpsc), dengan bantuan Arc dan Mutex untuk akses bersama yang aman. Hasilnya, request lambat tidak lagi memblokir seluruh server.

# Commit Bonus Reflection notes
Fungsi inisialisasi diubah dari new ke build agar lebih aman. Sekarang build mengembalikan Result, sehingga jika ukuran pool tidak valid (0), akan menghasilkan PoolCreationError tanpa panic!. Ini mencegah program berhenti tiba-tiba dan sesuai best practice Rust.