# n8n Talenta Payslip Bulk Download

> ⚠️ **Disclaimer**: Project ini dibuat untuk **tujuan edukasi** dan pembelajaran tentang workflow automation menggunakan n8n. Gunakan dengan bijak dan sesuai dengan kebijakan penggunaan layanan Mekari Talenta.

Workflow n8n untuk download semua payslip dari Mekari Talenta secara otomatis dalam satu klik.

## Features

- ✅ Download semua payslip dalam satu tahun sekaligus
- ✅ Otomatis rename file dengan format yang rapi
- ✅ Simpan ke folder lokal
- ✅ Tidak perlu install dependency tambahan

## Prerequisites

- Docker dan Docker Compose
- Akun Mekari Talenta

## Quick Start

### 1. Clone Repository

```bash
git clone https://github.com/semlakune/talenta-payslip-bulk-download.git
cd talenta-payslip-bulk-download
```

### 2. Jalankan n8n

```bash
docker compose up -d
```

Tunggu beberapa detik, lalu akses n8n di: http://localhost:5678

### 3. Setup Workflow

1. Buka http://localhost:5678
2. Buka workflow **"Talenta Download Payslip"**
3. Klik node **Config**
4. Isi parameter:
   - **year**: Tahun payslip yang ingin di-download (contoh: `2025`)
   - **cookie**: Cookie session dari browser Anda (lihat cara di bawah)

### 4. Cara Mendapatkan Cookie

1. Buka browser dan login ke https://hr.talenta.co
2. Buka **Developer Tools** (tekan `F12` atau `Cmd+Option+I` di Mac)
3. Pergi ke tab **Application** (Chrome) atau **Storage** (Firefox)
4. Di sidebar kiri, klik **Cookies** > `https://hr.talenta.co`
5. **Copy semua cookies** sebagai string dengan format: `nama1=nilai1; nama2=nilai2; ...`

**Cara cepat copy cookie:**

1. Buka tab **Network** di Developer Tools
2. Refresh halaman hr.talenta.co
3. Klik request pertama (biasanya nama file atau `payslip`)
4. Di panel kanan, cari **Request Headers** > **Cookie**
5. Copy seluruh nilai cookie

### 5. Jalankan Workflow

1. Paste cookie ke field **cookie** di node Config
2. Set **year** ke tahun yang diinginkan
3. Klik tombol **Execute Workflow**
4. Payslip akan di-download ke folder `payslips/`

## Output

Payslip akan tersimpan di folder `payslips/` dengan format nama:

```
Payslip-{id}-{month}-{year}.pdf
```

## Struktur Folder

```
.
├── docker-compose.yml    # Docker configuration
├── .env                  # Environment variables (optional)
├── n8n/
│   └── workflows/        # Workflow definitions
└── payslips/             # Downloaded payslips (output)
```

## Troubleshooting

### Error: "Invalid login credentials" atau 401

Cookie sudah expired. Dapatkan cookie baru dari browser setelah login ulang.

### Error: "No payslip data found"

- Pastikan cookie masih valid
- Pastikan tahun yang diset ada payslip-nya
- Coba akses hr.talenta.co di browser untuk memastikan masih login

### Payslip tidak ter-download

- Pastikan folder `payslips/` sudah ada
- Cek permission folder

## Commands

```bash
# Start n8n
docker compose up -d

# Stop n8n
docker compose down

# View logs
docker compose logs -f

# Restart (tanpa hapus data)
docker compose restart
```

## Notes

- Cookie session Talenta biasanya expired dalam beberapa jam
- Jalankan workflow segera setelah mendapatkan cookie
- Workflow ini tidak menyimpan password Anda - hanya menggunakan session cookie

## License

MIT
