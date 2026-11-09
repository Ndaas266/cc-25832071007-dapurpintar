# Catatan Evidence M03

## Penyimpangan dari modul
- Provider: IDCloudHost (bukan Azure). Modul M03 vendor-neutral sehingga langkah VPS tetap berlaku.
- Spesifikasi VPS aktual: 2 vCPU, 2 GB RAM, 20 GB disk. Modul mengasumsikan 1 vCPU dan 1 GB RAM. Gunicorn tetap memakai 1 worker dan 2 thread.
- File pengaturan SSH dinamai `00-pti2802.conf`, bukan `99-pti2802.conf`. Alasan: `50-cloud-init.conf` menyetel `PasswordAuthentication yes`, dan OpenSSH memakai nilai pertama yang dibaca. Nama `00-` memastikan `PasswordAuthentication no` yang berlaku. Dibuktikan dengan `sshd -T`.
- Deploy key GitHub dipasang dengan izin tulis (Read/write) sementara, karena push pertama dilakukan dari VPS. Rencana: ganti ke read-only setelah rilis M03.

## Hal yang teramati
- Gunicorn mencatat `Control server error: Permission denied` pada `/home/cloudstudent`. Aplikasi tetap sehat dan `/health` menjawab 200. Dugaan penyebab: `ProtectHome=true` pada service (belum diverifikasi lebih lanjut).
- VPS menyala ulang selama praktik (waktu mulai service berubah). Caddy dan `cc-m03` aktif kembali otomatis (`enabled`).
- Alamat IP publik tidak dicantumkan di repository (memakai placeholder `<PUBLIC_IP>`).

## Verifikasi keamanan
- Login SSH dengan key berhasil; login tanpa key ditolak (`Permission denied (publickey)`).
- UFW aktif: hanya 22/tcp dan 80/tcp.
- Gunicorn hanya mendengarkan di 127.0.0.1:8000.

## Perubahan proyek setelah rilis awal m03
- Proyek diganti dari "Asisten Belajar" menjadi "DapurPintar" (website rekomendasi masakan dari bahan yang tersedia). Nama repository diubah menjadi `cc-25832071007-dapurpintar`.
- Infrastruktur M03 (VPS, SSH key-only, UFW, Caddy, Gunicorn, systemd) tidak berubah, sehingga seluruh evidence server dan `/health` tetap berlaku.
- Yang diperbarui: halaman web, README, requirements (FR-01 sampai FR-07), architecture, dan ADR-0001.
- Rencana awal kajian DapurPintar (Node.js, Vercel, Supabase) tidak dipakai pada M03; alasan tercatat di ADR-0001. Keputusan database ditunda ke M05.
