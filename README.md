# 🚀 DevQuiz - Front-End Online Quiz App (React + Firebase)

Aplikasi kuis online interaktif seputar materi **Front-End Web Development** yang dibangun menggunakan **React 19**, **Vite**, dan terintegrasi dengan **Firebase Firestore**.

Proyek disimpan di: `D:\frontend-quiz-app`

---

## 🌟 Fitur Utama

1. **Materi Front-End Komprehensif**:
   - **HTML5 & Semantic Web**: Tag semantik, struktur dokumen, aksesibilitas.
   - **CSS3 & Layouts**: Box model, Flexbox, Grid, Specificity, Responsive Design.
   - **Modern JavaScript (ES6+)**: Scoping, Closures, Event Loop, Promises, Nullish Coalescing.
   - **React.js & Hooks**: Virtual DOM, `useState`, `useEffect`, `useRef`, `useMemo`, `useCallback`.
   - **Web APIs & Performance**: Storage (`localStorage` vs `sessionStorage`), Debounce vs Throttle, Core Web Vitals (CLS, LCP, INP).

2. **Pengalaman Pengguna (UX) Interaktif**:
   - ⏱️ **Timer Per Soal**: Mode 30 detik atau santai tanpa batas waktu.
   - 🔥 **Streak Counter**: Menghitung rentetan jawaban benar secara berturut-turut.
   - 🔊 **Web Audio Synthesizer**: Efek suara sintetis (correct chime, wrong buzz, fanfare) tanpa dependensi file eksternal audio dan dilengkapi tombol *Mute/Unmute*.
   - 🎉 **Canvas Confetti**: Animasi selebrasi confetti saat menyelesaikan kuis dengan skor memuaskan.
   - 📝 **Pembahasan Lengkap & Tinjauan Soal**: Setiap pertanyaan dilengkapi penjelasan konsep dan potongan kode (*code snippet*).
   - 🔁 **Ulangi Soal yang Salah**: Opsi langsung mengulang hanya pertanyaan yang keliru dijawab untuk mempercepat proses belajar.

3. **Integrasi Firebase + Fallback Cerdas**:
   - **Papan Peringkat (Cloud Leaderboard)**: Menyimpan rekor nilai, kategori, dan waktu ke Firestore `quiz_leaderboard`.
   - **Bank Soal Custom (Community Questions)**: Pengguna dapat menambah pertanyaan kuis baru yang tersinkron ke Cloud `quiz_questions`.
   - **Mode Offline Otomatis**: Jika kredensial Firebase belum dimasukkan atau koneksi internet terputus, aplikasi otomatis berjalan dengan mulus menggunakan `localStorage` tanpa error.
   - **Modal Pengaturan UI**: Anda dapat memasukkan/mengganti konfigurasi Firebase langsung melalui dialog pengaturan di layar tanpa perlu restart server.

4. **Keandalan & Penanganan Error**:
   - Dilengkapi dengan **React Error Boundary** (`ErrorBoundary.jsx`) untuk mencegah aplikasi crash dan menyediakan tombol pemulihan instan.

---

## 🛠️ Cara Menjalankan Aplikasi

Pastikan Node.js sudah terpasang di komputer Anda.

1. Buka Terminal / PowerShell di folder proyek:
   ```powershell
   cd D:\frontend-quiz-app
   ```

2. Jalankan development server:
   ```powershell
   npm run dev
   ```

3. Buka URL yang muncul di browser Anda (biasanya `http://localhost:5173`).

4. Untuk membuat versi production build:
   ```powershell
   npm run build
   ```

---

## 🌐 Menghubungkan ke Firebase Cloud (Opsional)

Aplikasi **sudah langsung dapat dimainkan** tanpa konfigurasi apapun berkat mode *Local Fallback*. Namun jika Anda ingin mengaktifkan sinkronisasi cloud:

1. Buat project baru gratis di [Firebase Console](https://console.firebase.google.com/).
2. Aktifkan **Firestore Database**:
   - Masuk ke menu **Build > Firestore Database** -> Klik **Create Database**.
   - Pilih mode **Test Mode** (agar aplikasi dapat menulis data leaderboard dan pertanyaan).
3. Aktifkan **Anonymous Authentication**:
   - Masuk ke menu **Build > Authentication** -> Tab **Sign-in method** -> Aktifkan **Anonymous**.
4. Ambil konfigurasi web app:
   - Klik ikon **Project Settings (gir)** di kiri atas > **General** > scroll ke bawah ke bagian **Your apps** > pilih icon Web (`</>`).
5. Sambungkan ke aplikasi:
   - **Cara 1 (Paling Mudah)**: Klik tombol ikon **Gir (Pengaturan)** di navbar aplikasi DevQuiz, lalu tempel (*paste*) kode `firebaseConfig` Anda, klik **Simpan & Sambungkan**.
   - **Cara 2**: Salin kredensial ke dalam file `.env` di folder proyek:
     ```env
     VITE_FIREBASE_API_KEY=AIzaSy...
     VITE_FIREBASE_AUTH_DOMAIN=project-id.firebaseapp.com
     VITE_FIREBASE_PROJECT_ID=project-id
     VITE_FIREBASE_STORAGE_BUCKET=project-id.appspot.com
     VITE_FIREBASE_MESSAGING_SENDER_ID=...
     VITE_FIREBASE_APP_ID=1:...
     ```

---

## 📁 Struktur Direktori

```
D:\frontend-quiz-app\
├── .env.example
├── .env
├── package.json
├── index.html
├── src\
│   ├── main.jsx
│   ├── index.css
│   ├── App.jsx
│   ├── App.css
│   ├── components\
│   │   ├── Navbar.jsx               # Header navigasi, audio toggle, status koneksi
│   │   ├── QuizStart.jsx            # Menu awal, pemilihan kategori, filter kesulitan
│   │   ├── QuizPlay.jsx             # Layar gameplay, timer, code block, feedback
│   │   ├── QuizResult.jsx           # Rangkuman skor, selebrasi confetti, accordion review
│   │   ├── Leaderboard.jsx          # Papan peringkat (Firestore & Local)
│   │   ├── AddQuestionModal.jsx     # Form penambahan pertanyaan baru
│   │   ├── FirebaseConfigModal.jsx  # Dialog pengaturan Firebase langsung di UI
│   │   └── ErrorBoundary.jsx        # Perlindungan error handling tingkat komponen
│   ├── data\
│   │   └── frontendQuestions.js     # Bank soal materi Front-End pilihan
│   ├── firebase\
│   │   ├── config.js                # Inisialisasi Firebase & deteksi mode offline
│   │   └── quizService.js           # CRUD Firestore untuk skor & pertanyaan kuis
│   └── utils\
│       └── sound.js                 # Web Audio API Sound Synthesizer
```
