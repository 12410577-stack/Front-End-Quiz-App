# DevQuiz Front-End Platform

Aplikasi kuis interaktif modern yang telah dimigrasi dan dimodernisasi menggunakan **ReactJS**, **TypeScript**, **Firebase**, **REST API**, dan **Large Language Model (LLM)**.

---

## 🚀 Fitur & Integrasi Utama

### 1. ⚛️ ReactJS 19 & 🔷 TypeScript
- Seluruh kode komponen (`.tsx`), utilitas, model data, dan layanan (`.ts`) menggunakan **TypeScript** murni.
- Type definitions terpusat pada [`src/types/quiz.ts`](file:///D:/frontend-quiz-app/src/types/quiz.ts).
- Validasi compile-time penuh dengan `npm run typecheck` (`tsc --noEmit`) tanpa error.

### 2. 🔥 Firebase (Cloud Firestore & Auth) & 🔐 Fitur Autentikasi (Login/Register)
- Terletak pada [`src/firebase/`](file:///D:/frontend-quiz-app/src/firebase/) dan [`src/context/AuthContext.tsx`](file:///D:/frontend-quiz-app/src/context/AuthContext.tsx).
- **Multi-Method Login**:
  - **Login dengan Google**: Autentikasi satu klik menggunakan Google Popup via Firebase Auth.
  - **Email & Kata Sandi**: Registrasi akun baru dengan validasi dan login terenkripsi.
  - **Akun Demo / Uji Coba Cepat**: Tombol sekali klik untuk mengisi akun pengujian otomatis.
  - **Mode Tamu (Guest)**: Opsi bermain tanpa login akun dengan identitas sementara.
- **Profil Pengguna & Riwayat Kuis**:
  - Modal profil lengkap menampilkan statistik pribadi: total kuis diselesaikan, skor tertinggi, rata-rata akurasi, dan total waktu bermain.
  - Daftar riwayat kuis tersimpan secara spesifik untuk tiap pengguna.
  - Kemampuan mengubah nama tampilan (*display name*) pengguna secara langsung.
- **Leaderboard Cloud**: Skor kuis tersinkronisasi secara otomatis ke koleksi `quiz_leaderboard` di Cloud Firestore dan menandai baris milik pengguna yang sedang login.
- **Custom Question Bank**: Soal kuis kustom tersimpan dan otomatis mencatat nama kontributor dari akun yang sedang login.
- **Offline / Local Fallback**: Jika Firebase belum aktif atau jaringan offline, sistem autentikasi dan penyimpanan beralih ke penyimpanan lokal browser secara aman tanpa error.

### 3. 🌐 REST API (Open Trivia DB & Custom Endpoints)
- Terletak pada [`src/services/restApiService.ts`](file:///D:/frontend-quiz-app/src/services/restApiService.ts).
- **Pengambilan Soal Dinamis**: Menarik soal live seputar Computer Science & Web dari Open Trivia DB REST API via HTTP GET.
- Dekoding entitas HTML otomatis dan pengacakan opsi jawaban secara aman.
- Mendukung integrasi ke custom REST API JSON endpoint.

### 4. 🤖 Large Language Model (LLM) - Google Gemini & AI Assistant
- Terletak pada [`src/services/llmService.ts`](file:///D:/frontend-quiz-app/src/services/llmService.ts) dan [`src/components/AIQuestionGeneratorModal.tsx`](file:///D:/frontend-quiz-app/src/components/AIQuestionGeneratorModal.tsx).
- **AI Question Generator**: Pengguna dapat memasukkan topik apa saja (contoh: *"React 19 Server Actions"*, *"TypeScript Generics"*, *"CSS Grid vs Flexbox"*), lalu LLM akan membuatkan soal, snippet kode, 4 opsi, dan pembahasan lengkap.
- **AI Pedagogical Hint**: Saat kuis berlangsung, pengguna dapat menekan tombol **"💡 Hint AI"** untuk memperoleh petunjuk pemikiran tanpa membocorkan jawaban langsung.
- **AI Deep Explanation (AI Tutor)**: Setelah menjawab atau pada layar tinjauan hasil, pengguna dapat meminta analisis mendalam dari AI Senior Mentor mengenai alasan teknis jawaban yang benar dan kesalahan umum.
- **Dual Engine**: Mendukung integrasi langsung ke Google Gemini API (`gemini-1.5-flash`, `gemini-2.0-flash`), serta dilengkapi **Intelligent Simulated AI** bawaan bila API Key belum diisi.

---

## 📁 Struktur Direktori Project

```
D:\frontend-quiz-app\
├── index.html
├── package.json
├── tsconfig.json
├── vite.config.js
└── src/
    ├── main.tsx
    ├── App.tsx
    ├── App.css
    ├── index.css
    ├── vite-env.d.ts
    ├── types/
    │   ├── quiz.ts                         # Type definitions kuis TypeScript
    │   └── auth.ts                         # Type definitions Autentikasi Pengguna
    ├── context/
    │   └── AuthContext.tsx                 # React Context untuk state autentikasi
    ├── services/
    │   ├── restApiService.ts               # Integrasi REST API HTTP
    │   └── llmService.ts                   # Integrasi Large Language Model (LLM)
    ├── firebase/
    │   ├── config.ts                       # Inisialisasi Firebase & Auth
    │   ├── authService.ts                  # Layanan login Google, Email & Guest
    │   └── quizService.ts                  # CRUD Firestore & LocalStorage
    ├── data/
    │   └── frontendQuestions.ts            # Bank soal bawaan front-end
    ├── utils/
    │   └── sound.ts                        # UI Sound Synthesizer Web Audio API
    └── components/
        ├── Navbar.tsx                      # Header navigasi & profil user
        ├── AuthModal.tsx                   # Modal Login / Registrasi Akun
        ├── UserProfileModal.tsx            # Modal Profil & Riwayat Kuis Pengguna
        ├── QuizStart.tsx                   # Layar setup kuis, REST API & AI
        ├── QuizPlay.tsx                    # Layar pengerjaan kuis + AI Hint
        ├── QuizResult.tsx                  # Layar hasil + AI Tutor Breakdown
        ├── Leaderboard.tsx                 # Papan peringkat Firestore
        ├── AddQuestionModal.tsx            # Form tambah soal manual
        ├── AIQuestionGeneratorModal.tsx    # Modal generator soal AI (LLM)
        ├── FirebaseConfigModal.tsx         # Modal pengaturan Firebase & LLM Key
        └── ErrorBoundary.tsx               # Penanganan error runtime
```

---

## 🛠️ Cara Menjalankan

### Menjalankan Mode Development:
```powershell
cd "D:\frontend-quiz-app"
npm run dev
```

### Type Checking TypeScript:
```powershell
npm run typecheck
```

### Build Produksi:
```powershell
npm run build
```
*(Menjalankan `tsc --noEmit` kemudian membundel dengan `vite build`)*.
