# Praktikum Komputasi Awan — Docker

Proyek ini merupakan implementasi praktikum Komputasi Awan yang mendemonstrasikan aplikasi inventaris multi-container dengan Docker Compose. Arsitektur terdiri dari web frontend, REST API, dan PostgreSQL.

## Repository

- **GitHub:** [willyrafaelfs/Praktikum-Komputasi-Awan-Docker](https://github.com/willyrafaelfs/praktikum-komputasi-awan-docker)
- **GitLab:** [willyrafaelfs/Praktikum-Komputasi-Awan-Docker](https://gitlab.com/willyrafaelfs/Praktikum-Komputasi-Awan-Docker)

Klon repository dari salah satu platform:

```bash
git clone https://github.com/willyrafaelfs/praktikum-komputasi-awan-docker.git
```

Atau gunakan mirror GitLab:

```bash
git clone https://gitlab.com/willyrafaelfs/Praktikum-Komputasi-Awan-Docker.git
```

## Fitur

- CRUD data inventaris (tambah, lihat, ubah, dan hapus).
- Pencarian realtime dan pengurutan kolom pada tabel.
- Ringkasan jumlah barang dan nilai inventaris.
- Pemisahan jaringan frontend dan backend; database tidak diekspos ke host.
- Healthcheck PostgreSQL dan volume untuk mempertahankan data.
- Mendukung scaling service API dengan Docker Compose.

## Teknologi

- **Frontend:** Python, Flask, CSS, dan JavaScript
- **API:** Python, Flask, dan Psycopg2
- **Database:** PostgreSQL 15
- **Container orchestration:** Docker Compose

Antarmuka menggunakan CSS lokal dan font sistem, sehingga styling tidak bergantung pada CDN eksternal.

## Menjalankan aplikasi

### Prasyarat

- Docker Desktop atau Docker Engine yang aktif.
- Docker Compose v2 (`docker compose`).

### Jalankan

Dari direktori repository, bangun image dan jalankan seluruh service:

```bash
docker compose up -d --build
```

Periksa status container:

```bash
docker compose ps
```

Buka frontend di [http://localhost:8000](http://localhost:8000).

Untuk melihat log:

```bash
docker compose logs -f
```

### Menghentikan aplikasi

Hentikan dan hapus container serta network:

```bash
docker compose down
```

Volume database tetap tersimpan dan akan digunakan kembali saat aplikasi dijalankan lagi. Untuk menghapus volume beserta seluruh data inventaris, jalankan:

```bash
docker compose down -v
```

## Arsitektur

- `web` melayani antarmuka pada port `8000` di host dan berkomunikasi dengan API melalui network frontend.
- `api` menyediakan operasi inventaris pada port `8080` dan terhubung ke kedua network.
- `db` menggunakan PostgreSQL dan hanya terhubung ke network backend.
- API menunggu healthcheck database sebelum dijalankan.

Untuk menjalankan dua instance API:

```bash
docker compose up -d --scale api=2
```
