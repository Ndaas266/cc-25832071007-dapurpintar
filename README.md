# DapurPintar

Cloud Computing — PTI 2802  
Pertemuan 3 — Project Inception

## Author
Amanda Fatihatul Ilmi / 25832071007 / 2A

## Problem
Pengguna sering kesulitan menentukan menu dari bahan makanan yang sudah tersedia, terutama pemula memasak dan pengguna dengan bahan terbatas. (Hipotesis, belum diverifikasi dengan survei.)

## Target Users
Mahasiswa dan anak kos, keluarga, pemula memasak, dan pengguna umum.

## Features M03
- baseline application
- health endpoint
- VPS deployment

## Planned Features
- input bahan makanan dan preferensi (waktu, porsi, pantangan)
- rekomendasi menu melalui AI API
- detail resep (bahan, takaran, langkah)
- riwayat resep

## Architecture

```mermaid
flowchart LR
    U[User] --> C[Caddy]
    C --> G[Gunicorn]
    G --> F[Flask]
```

## Infrastructure
- Ubuntu Server 24.04
- 2 vCPU
- 2 GB RAM
- 20 GB disk
- Caddy
- Gunicorn

## Public Endpoint
`http://<PUBLIC_IP>/`

## Health Check
`GET /health`

## Deployment
See `docs/deployment.md`.

## Security
- key-only SSH
- root SSH disabled
- UFW enabled
- backend loopback-only

## Current Limitations
- HTTP only
- no AI integration yet
- no persistent database
- no container
- manual deployment

## Roadmap
M04 DNS/HTTPS, M05 Data, M06 Container, M07 IaC, M09 CI/CD
