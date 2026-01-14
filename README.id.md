# 🚀 RajaOngkir MCP Server

<p align="center">
  <a href="README.md">🇬🇧 English</a> •
  <a href="README.id.md">🇮🇩 Bahasa Indonesia</a>
</p>

Server **Model Context Protocol (MCP)** untuk integrasi dengan **RajaOngkir Komerce V2 API** - cek ongkir dan lacak paket pengiriman Indonesia.

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://python.org)

---

## ✨ Fitur

- 🔍 **Pencarian Lokasi** - Cari kota/kecamatan domestik dan tujuan internasional
- 🗺️ **Lokasi Hierarkis** - Pilih lokasi bertahap (Provinsi → Kota → Kecamatan → Kelurahan)
- 💰 **Hitung Ongkir** - Kalkulasi biaya pengiriman domestik dan internasional
- 📦 **Lacak Paket** - Tracking pengiriman dari 20+ kurir Indonesia
- ⚡ **Multi-Kurir** - Bandingkan harga dari beberapa kurir sekaligus
- 🛡️ **Validasi Input** - Validasi otomatis untuk semua parameter
- 📋 **Response Standar** - Format JSON response yang konsisten

---

## 🚚 Kurir yang Didukung

**Domestik:** JNE, SiCepat, J&T, POS Indonesia, TIKI, AnterAja, Ninja Xpress, Lion Parcel, ID Express, dan 10+ lainnya

**Internasional:** POS Indonesia, JNE, TIKI, EMS

---

## 📦 Instalasi

### Prasyarat
- Python 3.10+
- API Key RajaOngkir Komerce ([Daftar di sini](https://rajaongkir.komerce.id))

### Setup

```bash
# Clone repository
git clone https://github.com/Arseno25/rajaongkir-mcp-server.git
cd rajaongkir-mcp-server

# Buat virtual environment
python -m venv .venv
.venv\Scripts\activate  # Windows
source .venv/bin/activate  # Linux/Mac

# Install dependencies
pip install -r requirements.txt

# Konfigurasi environment
cp .env.example .env
# Edit .env dan tambahkan RAJAONGKIR_API_KEY
```

---

## 🔌 Integrasi

### Claude Desktop

Tambahkan ke `claude_desktop_config.json`:

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

### MCP Inspector (Testing)

```bash
npx -y @modelcontextprotocol/inspector python server.py
```

---

## 🛠️ Tools yang Tersedia

<table>
  <thead>
    <tr>
      <th>Tool</th>
      <th>Deskripsi</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>search_domestic_destination</code></td>
      <td>Cari kota/kecamatan di Indonesia</td>
    </tr>
    <tr>
      <td><code>search_international_destination</code></td>
      <td>Cari negara tujuan internasional</td>
    </tr>
    <tr>
      <td><code>get_provinces</code></td>
      <td>Ambil daftar semua provinsi</td>
    </tr>
    <tr>
      <td><code>get_cities</code></td>
      <td>Ambil daftar kota dalam provinsi</td>
    </tr>
    <tr>
      <td><code>get_districts</code></td>
      <td>Ambil daftar kecamatan dalam kota</td>
    </tr>
    <tr>
      <td><code>get_subdistricts</code></td>
      <td>Ambil daftar kelurahan dalam kecamatan</td>
    </tr>
    <tr>
      <td><code>calculate_domestic_cost</code></td>
      <td>Hitung ongkir domestik</td>
    </tr>
    <tr>
      <td><code>calculate_district_cost</code></td>
      <td>Hitung ongkir pakai ID kecamatan (multi-kurir)</td>
    </tr>
    <tr>
      <td><code>calculate_international_cost</code></td>
      <td>Hitung ongkir internasional</td>
    </tr>
    <tr>
      <td><code>track_package</code></td>
      <td>Lacak paket dengan nomor resi</td>
    </tr>
  </tbody>
</table>

---

## 💡 Contoh Penggunaan

### Dengan Claude

> "Hitung ongkir dari Jakarta ke Surabaya untuk paket 1kg pakai JNE"

> "Lacak paket saya dengan resi JNE1234567890"

> "Tampilkan semua kota di provinsi DKI Jakarta"

> "Bandingkan harga kirim dari Jakarta ke Bandung pakai JNE, SiCepat, dan J&T"

---

## ⚙️ Konfigurasi

<table>
  <thead>
    <tr>
      <th>Environment Variable</th>
      <th>Wajib</th>
      <th>Deskripsi</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>RAJAONGKIR_API_KEY</code></td>
      <td align="center">✅</td>
      <td>API key RajaOngkir Komerce kamu</td>
    </tr>
    <tr>
      <td><code>RAJAONGKIR_BASE_URL</code></td>
      <td align="center">❌</td>
      <td>Base URL API (default: https://rajaongkir.komerce.id/api/v1)</td>
    </tr>
  </tbody>
</table>

---

## 📝 Lisensi

Proyek ini dilisensikan di bawah MIT License - lihat file [LICENSE](LICENSE) untuk detail.

---

## 🙏 Kredit

- [RajaOngkir Komerce](https://rajaongkir.komerce.id) - Penyedia API pengiriman
- [Model Context Protocol](https://modelcontextprotocol.io) - Spesifikasi MCP
