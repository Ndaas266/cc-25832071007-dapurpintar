# Requirements

## Problem Statement
Pengguna sering kesulitan menentukan menu dari bahan makanan yang sudah tersedia, terutama pemula memasak dan pengguna dengan bahan terbatas. Pengguna juga belum tentu mengetahui bahan tambahan yang benar-benar diperlukan. (Status: hipotesis, belum diverifikasi dengan survei.)

## Target Users
- Mahasiswa dan anak kos, keluarga, pemula memasak, dan pengguna umum.
- Pengelola: mahasiswa pengembang.

## Functional Requirements
- FR-01 Pengguna dapat memasukkan bahan makanan dan preferensi (jenis menu, waktu, porsi, pantangan) (rencana).
- FR-02 Sistem menghasilkan beberapa rekomendasi menu melalui AI API (rencana).
- FR-03 Endpoint GET /health (tersedia pada M03).
- FR-04 Sistem menampilkan detail resep: bahan, takaran, dan langkah memasak (rencana).
- FR-05 Sistem membatasi jumlah permintaan per pengguna untuk mengendalikan biaya AI (rencana).
- FR-06 Pengguna dapat melihat riwayat resep (rencana, M05).
- FR-07 Sistem menangani galat AI API (timeout, kuota habis) dengan pesan yang jelas (rencana).

## Non-Functional Requirements
- NFR-01 backend loopback-only
- NFR-02 application managed by systemd
- NFR-03 public request through reverse proxy
- NFR-04 no secret in repository; API key AI hanya di environment server

## Constraints
- Acuan modul: 1 vCPU, 1 GB RAM, 20 GB disk
- VPS aktual: 2 vCPU, 2 GB RAM, 20 GB disk
- Ubuntu Server 24.04
- public IPv4

## Acceptance Criteria M03
- [x] first deployment accessible
- [x] health endpoint works
