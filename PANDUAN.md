# Panduan Pemakaian Taktiva

## A. Menjalankan di komputer
1. Pasang Node.js 22. Ekstrak zip, buka terminal di foldernya.
2. `corepack enable` lalu `pnpm install`
3. `pnpm dev`, buka alamat yang tampil (mis. http://localhost:5173).
   Chat akan berjalan dalam **mode demo** (jawaban simulasi) karena `/api/chat` hanya aktif di Vercel.

## B. Online + chat AI sungguhan (Vercel)
1. Unggah folder ke GitHub, lalu "Import Project" di vercel.com (Framework: Vite).
2. Di Settings > Environment Variables isi `LLM_API_KEY` (kunci API Anthropic) dan opsional `LLM_MODEL`.
3. Deploy. Fungsi `api/chat.ts` otomatis aktif; kunci tidak pernah dikirim ke browser.
   Tanpa kunci, chat tetap jalan dengan label "Respons simulasi — mode demo".

## C. Alur demo (siswa Nadia)
1. Landing > "Mulai Perjalananmu" > daftar/masuk > onboarding.
2. Kenali Dirimu: jawab asesmen. Hasilnya sinyal eksplorasi, bukan tes psikologi.
3. Eksplorasi Jurusan: simpan jurusan dengan ikon bookmark, buka detail.
4. Career Challenge: kerjakan Data Analysis, isi refleksi, lihat hasil.
5. Taktiva AI (tombol mengambang): tanya "Apakah perlu jago matematika untuk jurusan data?"
6. Simulasi Masa Depan: ubah budget/kesiapan/lokasi dan lihat perubahannya.
7. Bandingkan Pendidikan lalu Roadmap Saya: centang tugas, progres ikut naik.
8. Tersimpan dan Profil: tinjau pilihan dan ubah preferensi.

## D. Catatan penting
- Data kampus dan biaya adalah **contoh**; selalu verifikasi di situs resmi.
- Progres disimpan di browser (localStorage, awalan `taktiva:`). Reset: DevTools > Application > Local Storage.
- Jangan memasukkan data sensitif; ini prototipe tanpa login sungguhan.

## E. Alternatif: deploy di Netlify
1. Unggah folder ke GitHub (termasuk `netlify/` dan `netlify.toml`).
2. Di app.netlify.com: Add new site > Import an existing project > pilih repositori.
3. Build command `pnpm build` dan publish directory `dist` sudah diatur di `netlify.toml`.
4. Site configuration > Environment variables: isi `LLM_API_KEY` (dan opsional `LLM_MODEL`), lalu deploy ulang.
5. Fungsi `netlify/functions/chat.ts` otomatis melayani `/api/chat`. Folder `api/` hanya untuk Vercel dan diabaikan Netlify.
