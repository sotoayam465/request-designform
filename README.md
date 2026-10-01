# Fortunagrande Studio — Design Request (GitHub Pages)

Arsitektur: **frontend** (`index.html`, `admin.html`) di GitHub Pages → memanggil **API** Google Apps Script (`Code.gs`) → Sheets / Drive / Calendar / WhatsApp.

## A. Update backend Apps Script
1. Buka project Apps Script Anda.
2. Ganti seluruh isi `Code.gs` dengan file `apps-script/Code.gs`.
3. **Hapus** file `Index` dan `Admin` (HTML) dari project Apps Script — sudah tidak dipakai.
4. Simpan token Fonnte: di `setFonnteToken()` tempel token, Run sekali, lalu hapus token dari kode.
5. Deploy → **Manage deployments** → ikon pensil pada deployment yang ada → Version: **New version** → Deploy.
   Pastikan *Execute as: Me* dan *Who has access: Anyone*. Dengan cara ini URL `/exec` tetap sama.
6. Tes: buka URL `/exec` di browser. Harus muncul `{"ok":true,"service":"Fortunagrande Studio — Design Request API"}`.
7. Jika Anda membuat deployment BARU (URL berubah), ganti `API_URL` di dalam `index.html` dan `admin.html`.

## B. Publish ke GitHub Pages
1. Buat repo baru di GitHub, mis. `design-request`.
2. Upload **hanya** `index.html`, `admin.html`, dan `README.md` (jangan upload `Code.gs`).
3. Repo → **Settings → Pages** → Source: *Deploy from a branch* → Branch `main`, folder `/ (root)` → Save.
4. Tunggu 1–2 menit. Alamat: `https://<username>.github.io/design-request/` (form) dan `.../admin.html` (admin).

## C. Domain sendiri (opsional)
Settings → Pages → Custom domain, mis. `request.fortunagrande-jember.com`. Tambahkan record `CNAME` di DNS ke `<username>.github.io`, lalu centang *Enforce HTTPS*.

## D. Catatan
- Repo **public** aman karena HTML hanya berisi URL API (tanpa token/ID sheet). Repo private baru bisa memakai Pages jika akun GitHub berbayar.
- Admin tetap tanpa login (sesuai keputusan awal). Siapa pun yang tahu alamat `admin.html` bisa membukanya; jangan sebar link-nya.
- Setiap mengubah `Code.gs`, deploy ulang dengan *New version*, kalau tidak perubahan tidak aktif.

## Troubleshooting
| Gejala | Penyebab / solusi |
|---|---|
| "Gagal memuat" / error CORS di konsol | Akses deployment belum *Anyone*, atau belum deploy *New version* |
| Halaman Google minta login | Sama: set *Who has access: Anyone* |
| `Action tidak dikenal` | Frontend lebih baru dari backend → deploy ulang `Code.gs` |
| Gambar gagal terkirim | Ukuran total terlalu besar; kurangi jumlah gambar (maks 5) |
| Perubahan di GitHub belum tampil | Tunggu build Pages, lalu hard refresh (Ctrl+F5) |
