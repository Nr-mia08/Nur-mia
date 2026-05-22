# Nur-mia<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Teman Curhat Terbaikmu</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #f2f9f5; /* Putih dengan sentuhan hijau super lembut */
            color: #2c4c3e;
            overflow: hidden;
        }

        .card {
            background-color: #ffffff;
            padding: 40px;
            border-radius: 24px;
            box-shadow: 0 12px 40px rgba(44, 76, 62, 0.08);
            text-align: center;
            max-width: 480px;
            width: 90%;
            border: 2px solid #e1f2e9;
            position: relative;
            transition: all 0.3s ease;
        }

        .sticker-container {
            font-size: 75px;
            margin-bottom: 20px;
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-12px); }
        }

        h1 {
            font-size: 1.8rem;
            margin-bottom: 15px;
            color: #1b4332;
            font-weight: 700;
        }

        p {
            font-size: 1rem;
            line-height: 1.6;
            margin-bottom: 30px;
            color: #52796f;
        }

        .btn-group {
            display: flex;
            justify-content: center;
            gap: 20px;
            position: relative;
            min-height: 50px;
        }

        button {
            padding: 14px 32px;
            font-size: 1rem;
            font-weight: 600;
            border-radius: 50px;
            cursor: pointer;
            border: none;
            transition: all 0.2s ease;
            box-shadow: 0 4px 12px rgba(44, 76, 62, 0.1);
        }

        #btn-oke {
            background-color: #2d6a4f; /* Hijau Daun Teduh */
            color: white;
        }

        #btn-oke:hover {
            background-color: #1b4332;
            transform: scale(1.05);
        }

        #btn-tidak {
            background-color: #e8f5e9; /* Hijau sangat muda agar senada */
            color: #2d6a4f;
            position: absolute;
            left: calc(50% + 15px); 
        }

        /* Saat tombol "Tidak" mulai mendeteksi kursor/sentuhan dan menghindar */
        #btn-tidak.running {
            position: fixed;
            z-index: 999;
            transition: all 0.12s ease-out;
            background-color: #ffebeb; /* Berubah sedikit kemerahan saat mencoba kabur */
            color: #c94c4c;
        }

        /* Area Pesan Sukses / Solusi Curhat */
        .pesan-sukses {
            display: none;
        }

        .pesan-sukses h2 {
            color: #1b4332;
            margin-bottom: 15px;
            font-size: 1.6rem;
        }

        .quote-box {
            background-color: #f4faf7;
            border-left: 4px solid #40916c;
            padding: 15px;
            border-radius: 8px;
            text-align: left;
            margin-top: 20px;
            font-style: italic;
        }
    </style>
</head>
<body>

    <div class="card">
        <!-- Tampilan Awal: Penawaran Curhat -->
        <div id="konten-pertanyaan">
            <div class="sticker-container" id="sticker">🧸💚</div>
            <h1>Butuh Teman Curhat & Saran?</h1>
            <p>Hai! Kalau harimu terasa berat, membingungkan, atau kamu cuma butuh seseorang untuk mendengarkan tanpa menghakimi... aku ada di sini untukmu. Mau cerita sekarang?</p>
            
            <div class="btn-group">
                <button id="btn-oke">Oke</button>
                <button id="btn-tidak">Tidak</button>
            </div>
        </div>

        <!-- Tampilan Setelah Klik Oke (Pesan Positif & Saran) -->
        <div id="konten-sukses" class="pesan-sukses">
            <div class="sticker-container">☕✨</div>
            <h2>Pintu Selalu Terbuka Untukmu</h2>
            <p>Terima kasih sudah mau berbagi! Menahan semuanya sendirian itu melelahkan, dan bercerita adalah langkah awal yang luar biasa hebat.</p>
            
            <div class="quote-box">
                "Ingat ya, tidak apa-apa untuk merasa tidak baik-baik saja. Kamu tidak harus menyelesaikan atau memikirkan semuanya hari ini. Ambil napas dalam-dalam, mari kita cari solusinya pelan-pelan bersama." 🍀
            </div>
        </div>
    </div>

    <script>
        const btnTidak = document.getElementById('btn-tidak');
        const btnOke = document.getElementById('btn-oke');
        const kontenPertanyaan = document.getElementById('konten-pertanyaan');
        const kontenSukses = document.getElementById('konten-sukses');
        const sticker = document.getElementById('sticker');

        // Variasi stiker/emoji yang berganti saat tombol "Tidak" coba didekati
        const stikerKabur = ['🥺👉👈', '🤫🍃', '🙈💨', '🎧❌', '🤷‍♂️💚'];

        // Fungsi acak posisi tombol
        function lariDariKenyataan() {
            if (!btnTidak.classList.contains('running')) {
                btnTidak.classList.add('running');
            }

            // Hitung ruang aman agar tombol tidak tenggelam ke luar layar browser
            const batasAman = 30;
            const maxX = window.innerWidth - btnTidak.offsetWidth - batasAman;
            const maxY = window.innerHeight - btnTidak.offsetHeight - batasAman;

            // Koordinat acak baru
            const randomX = Math.max(batasAman, Math.floor(Math.random() * maxX));
            const randomY = Math.max(batasAman, Math.floor(Math.random() * maxY));

            btnTidak.style.left = `${randomX}px`;
            btnTidak.style.top = `${randomY}px`;

            // Ganti stiker secara acak untuk efek interaktif interaksi curhat
            const stikerAcak = stikerKabur[Math.floor(Math.random() * stikerKabur.length)];
            sticker.textContent = stikerAcak;
        }

        // Responsif untuk Komputer (Mouse) dan HP (Sentuhan Jari)
        btnTidak.addEventListener('mouseover', lariDariKenyataan);
        btnTidak.addEventListener('touchstart', function(e) {
            e.preventDefault(); // Mencegah klik bawaan mobile sebelum sempat pindah posisi
            lariDariKenyataan();
        });

        // Aksi ketika bersedia curhat (Klik Oke)
        btnOke.addEventListener('click', () => {
            kontenPertanyaan.style.display = 'none';
            kontenSukses.style.display = 'block';
            
            // Lenyapkan tombol tidak yang mungkin sedang bersembunyi di pojok layar
            btnTidak.style.display = 'none'; 
        });
    </script>
</body>
</html>
