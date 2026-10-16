# Taktiva — Temukan Arah, Wujudkan Masa Depan

Prototipe platform panduan pendidikan & karier untuk siswa SMA kelas XII (Bahasa Indonesia).
Stack yang ada di proyek ini: React 19 + Vite + Tailwind v4 + Lucide.

## Menjalankan
    corepack enable
    pnpm install
    pnpm dev        # buka alamat yang tampil di terminal
    pnpm build      # build produksi ke folder dist/ (bisa di-deploy ke Netlify/Vercel/Cloudflare Pages)

## Supabase Auth + profil online
Aplikasi dapat berjalan dalam dua mode:
- **Online:** jika `VITE_SUPABASE_URL` dan `VITE_SUPABASE_ANON_KEY` diisi, login/registrasi menggunakan Supabase Auth dan profil disimpan ke tabel `public.profiles`.
- **Demo lokal:** jika env tersebut belum diisi, aplikasi tetap memakai akun lokal untuk demo. Ini bukan autentikasi produksi.

### Menyiapkan Supabase
1. Buat proyek di https://supabase.com/ dan buka Project Settings → API. Salin Project URL dan publishable/anon key. Jangan pernah gunakan `service_role` key di frontend.
2. Salin `.env.example` menjadi `.env.local`, lalu isi `VITE_SUPABASE_URL` dan `VITE_SUPABASE_ANON_KEY`.
3. Di Supabase Dashboard → SQL Editor, jalankan isi `supabase/schema.sql`. Ini membuat tabel profil dan Row Level Security agar pengguna hanya dapat mengakses profilnya sendiri.
4. Jalankan `pnpm install`, `pnpm dev`. Untuk production, tambahkan dua variabel `VITE_SUPABASE_URL` dan `VITE_SUPABASE_ANON_KEY` pada pengaturan Environment Variables di Vercel, lalu redeploy.
5. Di Supabase → Authentication → URL Configuration, set Site URL ke URL deploy Vercel dan tambahkan URL deploy itu ke Redirect URLs. Untuk verifikasi email, atur SMTP/email provider sesuai kebutuhan.

Reset kata sandi mengirim email Supabase jika pengguna mengisi emailnya. Login Google belum diimplementasikan; aktifkan provider di Supabase saja belum cukup tanpa menambahkan OAuth flow di aplikasi.

Semua data rekomendasi adalah contoh lokal. Respons Taktiva AI berasal dari balasan simulasi di `getAIReply`
(bukan LLM sungguhan). Data kampus dan biaya adalah contoh, wajib diverifikasi ke situs resmi.

## Penyimpanan lokal
Progres (halaman, jurusan tersimpan, centang roadmap, setelan simulator, challenge selesai, riwayat chat) disimpan di `localStorage` browser dengan awalan `taktiva:`. Data hanya ada di perangkat itu; hapus lewat DevTools > Application > Local Storage. Jangan menyimpan data sensitif di sini.

## Belum tersedia (perlu dikerjakan berikutnya)
- OAuth Google dan pengelolaan email akun masih perlu konfigurasi/implementasi lanjutan.
- `/api/chat` sudah ada (lihat PANDUAN.md) tapi belum diuji; hanya aktif di Vercel.
- Rute URL terpisah (`/dashboard`, `/majors/[id]`, dll.): saat ini navigasi berbasis state.
- Aplikasi ini Vite, bukan Next.js App Router seperti di spesifikasi.

## Fitur akun yang sudah disiapkan
- Registrasi dan login melalui Supabase Auth jika konfigurasi tersedia.
- Verifikasi email mengikuti pengaturan Supabase project.
- Reset kata sandi melalui email dan form untuk menetapkan kata sandi baru.
- Profil siswa tersimpan di tabel `profiles`; onboarding dan edit profil melakukan upsert ke database.
- Row Level Security membatasi akses profil hanya untuk pemilik akun.
- Jika Supabase belum dikonfigurasi, aplikasi masih dapat dijalankan dalam mode demo lokal.

**Batasan:** integrasi Supabase belum bisa diuji end-to-end tanpa URL/key proyek milikmu. Login Google belum diimplementasikan. Progres fitur lain (jurusan tersimpan, roadmap, challenge, dan riwayat chat) masih disimpan lokal. Rekomendasi jurusan/karier masih data contoh, jadi verifikasi informasi kampus dan biaya dari sumber resmi.
