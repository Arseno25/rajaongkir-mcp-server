# RajaOngkir MCP Server

<p align="center">
  <a href="README.md">🇬🇧 English</a> •
  <a href="README.id.md">🇮🇩 Bahasa Indonesia</a>
</p>

Server [Model Context Protocol (MCP)](https://modelcontextprotocol.io) yang ringan untuk mengintegrasikan AI assistant seperti Claude dan Cursor dengan RajaOngkir API - cek ongkir dan lacak paket Indonesia.

- [Contoh Interaksi](#contoh-interaksi)
- [Tools](#tools)
  - [Pencarian Lokasi](#pencarian-lokasi)
  - [Lokasi Hierarkis](#lokasi-hierarkis)
  - [Kalkulasi Ongkir](#kalkulasi-ongkir)
  - [Lacak Paket](#lacak-paket)
- [Setup](#setup)
  - [Prasyarat](#prasyarat)
  - [Instalasi](#instalasi)
  - [Konfigurasi](#konfigurasi)
- [Integrasi dengan Claude Desktop dan Cursor](#integrasi-dengan-claude-desktop-dan-cursor)

## Contoh Interaksi

- "Hitung ongkir dari Jakarta ke Surabaya untuk paket 1kg"
- "Bandingkan harga JNE, SiCepat, dan J&T dari Bandung ke Yogyakarta"
- "Lacak paket saya dengan resi JNE1234567890"
- "Tampilkan semua kecamatan di Jakarta Pusat"

## Tools

### Pencarian Lokasi

1. **searchDomesticDestination**
   - Deskripsi: Cari kota/kecamatan di Indonesia
   - Parameter:
     - `query` (string): Nama lokasi yang dicari
   - Return: Daftar lokasi yang cocok beserta ID
   - Contoh: `searchDomesticDestination("Jakarta")`

2. **searchInternationalDestination**
   - Deskripsi: Cari negara tujuan internasional
   - Parameter:
     - `query` (string): Nama negara yang dicari
   - Return: Daftar negara yang cocok beserta ID
   - Contoh: `searchInternationalDestination("Singapore")`

### Lokasi Hierarkis

3. **getProvinces**
   - Deskripsi: Ambil semua provinsi Indonesia
   - Parameter: Tidak ada
   - Return: Daftar provinsi beserta ID
   - Contoh: `getProvinces()`

4. **getCities**
   - Deskripsi: Ambil kota dalam provinsi
   - Parameter:
     - `province_id` (string): ID provinsi
   - Return: Daftar kota beserta ID
   - Contoh: `getCities("6")` (DKI Jakarta)

5. **getDistricts**
   - Deskripsi: Ambil kecamatan dalam kota
   - Parameter:
     - `city_id` (string): ID kota
   - Return: Daftar kecamatan beserta ID
   - Contoh: `getDistricts("152")` (Jakarta Pusat)

6. **getSubdistricts**
   - Deskripsi: Ambil kelurahan dalam kecamatan
   - Parameter:
     - `district_id` (string): ID kecamatan
   - Return: Daftar kelurahan beserta ID
   - Contoh: `getSubdistricts("2096")`

### Kalkulasi Ongkir

7. **calculateDomesticCost**
   - Deskripsi: Hitung ongkir domestik menggunakan ID lokasi dari pencarian
   - Parameter:
     - `origin` (string): ID lokasi asal
     - `destination` (string): ID lokasi tujuan
     - `weight` (int): Berat paket dalam gram
     - `courier` (string): Kode kurir (jne, sicepat, jnt, pos, tiki, dll)
   - Return: Pilihan ongkos kirim
   - Contoh: `calculateDomesticCost("12345", "67890", 1000, "jne")`

8. **calculateDistrictCost**
   - Deskripsi: Hitung ongkir menggunakan ID kecamatan (mendukung multi kurir)
   - Parameter:
     - `origin` (string): ID kecamatan asal
     - `destination` (string): ID kecamatan tujuan
     - `weight` (int): Berat paket dalam gram
     - `courier` (string): Kode kurir dipisah titik dua
   - Return: Pilihan ongkos kirim dari semua kurir
   - Contoh: `calculateDistrictCost("1391", "1376", 1000, "jne:sicepat:jnt")`

9. **calculateInternationalCost**
   - Deskripsi: Hitung ongkir internasional
   - Parameter:
     - `origin` (string): ID lokasi asal (Indonesia)
     - `destination` (string): ID negara tujuan
     - `weight` (int): Berat paket dalam gram
     - `courier` (string): Kode kurir (pos, jne, tiki, ems)
   - Return: Pilihan ongkos kirim internasional
   - Contoh: `calculateInternationalCost("12345", "108", 1000, "pos")`

### Lacak Paket

10. **trackPackage**
    - Deskripsi: Lacak paket berdasarkan nomor resi
    - Parameter:
      - `awb` (string): Nomor resi
      - `courier` (string): Kode kurir
    - Return: Status tracking dan riwayat pengiriman
    - Contoh: `trackPackage("JNE1234567890", "jne")`

## Setup

### Prasyarat

- Python 3.10+
- API Key RajaOngkir Komerce

### Instalasi

```bash
git clone https://github.com/Arseno25/rajaongkir-mcp-server.git
cd rajaongkir-mcp-server
pip install -r requirements.txt
```

### Konfigurasi

Buat file `.env` di root project (bisa copy dari contoh):

```bash
cp .env.example .env
```

Edit file dengan API key kamu:

```env
RAJAONGKIR_API_KEY=api-key-kamu
RAJAONGKIR_BASE_URL=https://rajaongkir.komerce.id/api/v1
```

### Mendapatkan API Key RajaOngkir

1. Buka [RajaOngkir Komerce](https://rajaongkir.komerce.id)
2. Buat akun atau login
3. Subscribe ke paket (ada paket gratis)
4. Copy API key dari dashboard

## Integrasi dengan Claude Desktop dan Cursor

Untuk menggunakan MCP server ini dengan Claude Desktop, tambahkan ke konfigurasi Claude (`claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "rajaongkir": {
      "command": "python",
      "args": ["path/to/rajaongkir-mcp-server/server.py"],
      "env": {
        "RAJAONGKIR_API_KEY": "api-key-kamu"
      }
    }
  }
}
```

Untuk Cursor, buka tab MCP di Cursor Settings. Tambahkan server dengan command:

```
python path/to/rajaongkir-mcp-server/server.py
```

### Kurir yang Didukung

**Domestik:** JNE, SiCepat, J&T, POS Indonesia, TIKI, AnterAja, Ninja Xpress, Lion Parcel, ID Express, SAP, NCS, REX, RPX, Wahana, dan lainnya.

**Internasional:** POS Indonesia, JNE, TIKI, EMS

## Lisensi

Proyek ini dilisensikan di bawah MIT License - lihat file [LICENSE](LICENSE) untuk detail.
