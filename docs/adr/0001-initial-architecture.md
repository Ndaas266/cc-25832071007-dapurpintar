# ADR-0001: Initial VPS Deployment Architecture

## Status
Accepted

## Context
Proyek DapurPintar (website rekomendasi masakan dari bahan yang tersedia, dengan AI API). VPS Ubuntu Server 24.04 di IDCloudHost dengan 2 vCPU, 2 GB RAM, dan 20 GB disk (modul mengasumsikan 1 vCPU dan 1 GB RAM). Modul M03 meminta deployment pertama pada VPS. Aplikasi awal adalah baseline Flask yang sudah berjalan.

## Decision
- Flask
- Gunicorn 1 worker, 2 thread
- systemd
- Caddy
- UFW
- GitHub

## Alternatives
1. Node.js + Vercel + Supabase (rencana awal pada kajian DapurPintar)
2. Node.js + PM2 di VPS
3. NGINX + Gunicorn
4. Docker
5. PHP-FPM

## Rationale
- Deployment pada VPS adalah syarat M03; Vercel dan Supabase tidak menggantikan syarat tersebut, sehingga alternatif 1 tidak dipakai pada M03.
- Flask dipilih karena baseline sudah berjalan dan terverifikasi; membangun ulang dengan Node.js tidak menambah nilai pada tahap ini. Pemanggilan AI API dari Flask bersifat I/O-bound.
- Gunicorn memakai 1 worker dan 2 thread agar penggunaan memori rendah dan tersisa ruang untuk sistem.
- systemd menjalankan aplikasi di latar belakang, menyala otomatis setelah restart, dan dihidupkan ulang saat gagal.
- Caddy sebagai pintu masuk publik karena konfigurasinya singkat dan mendukung HTTPS otomatis pada M04.
- UFW membatasi port masuk hanya SSH dan HTTP.
- Docker ditunda ke M06 untuk menjaga baseline tetap sederhana dan hemat sumber daya.
- Pilihan database (SQLite atau layanan terkelola seperti Supabase) ditunda ke M05 dan akan dicatat pada ADR tersendiri.

## Consequences
### Positive
- Penggunaan sumber daya rendah (service sekitar 30-40 MB memori).
- Konfigurasi sederhana dan mudah dijelaskan.
- Aplikasi tetap hidup setelah logout dan restart VPS.
### Negative
- Deployment masih manual.
- Hanya satu VPS, tanpa redundansi.
- Hanya HTTP, belum terenkripsi.
- Belum ada database dan belum ada integrasi AI.
- Rencana teknologi pada kajian (Node.js, Vercel, Supabase) perlu disesuaikan dengan keputusan ini.

## Review Trigger
Review pada M05 (database dan integrasi AI) dan M06/M07.
