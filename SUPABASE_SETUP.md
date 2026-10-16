# Panduan mengaktifkan akun online Taktiva

## A. Buat proyek
1. Buka https://supabase.com/ lalu buat proyek baru.
2. Simpan password database di tempat aman; website tidak memerlukan password database tersebut.
3. Di Project Settings → API, salin Project URL dan publishable key/anon key.

## B. Siapkan tabel profil
1. Buka SQL Editor di dashboard Supabase.
2. Buka file `supabase/schema.sql` pada proyek ini, salin seluruh isinya, lalu jalankan.
3. Tabel `profiles` memakai `id` yang merujuk ke `auth.users` dan kebijakan RLS agar siswa hanya dapat membaca/mengubah profil sendiri.

## C. Hubungkan aplikasi lokal
1. Duplikat `.env.example` dan beri nama `.env.local`.
2. Isi: `VITE_SUPABASE_URL=https://...supabase.co` dan `VITE_SUPABASE_ANON_KEY=...`.
3. Jangan menambahkan `service_role` key ke variabel `VITE_*` atau commit `.env.local` ke GitHub.
4. Jalankan `pnpm install`, lalu `pnpm dev`.

## D. Atur email & URL
Di Authentication → URL Configuration, isi Site URL untuk alamat deploy dan tambahkan URL lokal `http://localhost:5173/**` serta URL Vercel ke Redirect URLs. Uji pendaftaran; bila verifikasi email aktif, pengguna harus membuka tautan email sebelum login.

## E. Deploy
Tambahkan `VITE_SUPABASE_URL` dan `VITE_SUPABASE_ANON_KEY` ke Project Settings → Environment Variables di Vercel untuk Preview dan Production, kemudian lakukan redeploy.

## Pengujian wajib
- Daftar dengan email yang dapat diakses.
- Verifikasi email jika diminta, lalu login.
- Lengkapi onboarding dan simpan profil.
- Refresh halaman dan login dari browser lain untuk memastikan data profil tetap tersedia.
- Buat dua akun dan pastikan akun A tidak bisa membaca/mengubah profil akun B.
- Uji reset kata sandi.

Catatan: mode lokal tetap tersedia bila environment variables tidak ada. Rekomendasi jurusan/karier di website masih data demo, bukan keputusan pendidikan profesional.
