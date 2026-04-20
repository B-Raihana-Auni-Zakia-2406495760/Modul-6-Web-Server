# Commit 1 Reflection notes
Pada tahap ini, saya mempelajari cara Rust menangani koneksi TCP sederhana dengan TcpListener yang di bind ke 127.0.0.1:7878 untuk menerima koneksi masuk. Setiap koneksi diproses lewat listener.incoming() dan ditangani oleh handle_connection. Data HTTP request dibaca menggunakan BufReader secara efisien, lalu dikumpulkan ke dalam vector agar mudah dipahami.

![Commit 2 screen capture](/assets/images/commit2.png)
# Commit 2 Reflection notes
Pada tahap ini, web server sudah bisa mengirim file HTML, bukan hanya mencetak request. File hello.html dibaca dengan fs::read_to_string, lalu dikirim sebagai response lengkap dengan HTTP/1.1 200 OK dan Content-Length. Semua digabung dengan format! dan dikirim ke stream agar bisa ditampilkan di browser.

![Commit 3 screen capture](/assets/images/commit3.png)
# Commit 3 Reflection notes
Server sekarang bisa memvalidasi request line dan memberi respons berbeda. Jika GET /, server mengembalikan hello.html dengan 200 OK. Jika path tidak dikenali (misalnya /bad), server mengirim 404 NOT FOUND dengan halaman bad.html.