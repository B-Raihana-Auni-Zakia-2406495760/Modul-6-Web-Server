# Commit 1 Reflection notes
Pada milestone ini, saya mempelajari cara Rust menangani koneksi TCP sederhana dengan TcpListener yang di bind ke 127.0.0.1:7878 untuk menerima koneksi masuk. Setiap koneksi diproses lewat listener.incoming() dan ditangani oleh handle_connection. Data HTTP request dibaca menggunakan BufReader secara efisien, lalu dikumpulkan ke dalam vector agar mudah dipahami.

