# 🚀 RajaOngkir MCP Server

<p align="center">
  <a href="README.md">🇬🇧 English</a> •
  <a href="README.id.md">🇮🇩 Bahasa Indonesia</a>
</p>

A **Model Context Protocol (MCP)** server that provides seamless integration with **RajaOngkir Komerce V2 API** for Indonesian shipping cost calculation and package tracking.

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://python.org)

---

## ✨ Features

- 🔍 **Location Search** - Search domestic cities/districts and international destinations
- 🗺️ **Hierarchical Location** - Step-by-step location selection (Province → City → District → Subdistrict)
- 💰 **Cost Calculation** - Calculate shipping costs for domestic and international deliveries
- 📦 **Package Tracking** - Track shipments across 20+ Indonesian couriers
- ⚡ **Multi-Courier Support** - Compare prices from multiple couriers at once
- 🛡️ **Input Validation** - Built-in validation for all parameters
- 📋 **Standardized Responses** - Consistent JSON response format

---

## 🚚 Supported Couriers

**Domestic:** JNE, SiCepat, J&T, POS Indonesia, TIKI, AnterAja, Ninja Xpress, Lion Parcel, ID Express, and 10+ more

**International:** POS Indonesia, JNE, TIKI, EMS

---

## 📦 Installation

### Prerequisites
- Python 3.10+
- RajaOngkir Komerce API Key ([Get it here](https://rajaongkir.komerce.id))

### Setup

```bash
# Clone the repository
git clone https://github.com/Arseno25/rajaongkir-mcp-server.git
cd rajaongkir-mcp-server

# Create virtual environment
python -m venv .venv
.venv\Scripts\activate  # Windows
source .venv/bin/activate  # Linux/Mac

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env
# Edit .env and add your RAJAONGKIR_API_KEY
```

---

## 🔌 Integration

### Claude Desktop

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "rajaongkir": {
      "command": "python",
      "args": ["path/to/rajaongkir-mcp-server/server.py"],
      "env": {
        "RAJAONGKIR_API_KEY": "your-api-key-here"
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

## 🛠️ Available Tools

<table>
  <thead>
    <tr>
      <th>Tool</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>search_domestic_destination</code></td>
      <td>Search for cities/districts in Indonesia</td>
    </tr>
    <tr>
      <td><code>search_international_destination</code></td>
      <td>Search for international countries</td>
    </tr>
    <tr>
      <td><code>get_provinces</code></td>
      <td>Get all Indonesian provinces</td>
    </tr>
    <tr>
      <td><code>get_cities</code></td>
      <td>Get cities within a province</td>
    </tr>
    <tr>
      <td><code>get_districts</code></td>
      <td>Get districts within a city</td>
    </tr>
    <tr>
      <td><code>get_subdistricts</code></td>
      <td>Get subdistricts within a district</td>
    </tr>
    <tr>
      <td><code>calculate_domestic_cost</code></td>
      <td>Calculate domestic shipping cost</td>
    </tr>
    <tr>
      <td><code>calculate_district_cost</code></td>
      <td>Calculate cost using district IDs (multi-courier)</td>
    </tr>
    <tr>
      <td><code>calculate_international_cost</code></td>
      <td>Calculate international shipping cost</td>
    </tr>
    <tr>
      <td><code>track_package</code></td>
      <td>Track package by AWB number</td>
    </tr>
  </tbody>
</table>

---

## 💡 Example Usage

### With Claude

> "Calculate shipping cost from Jakarta to Surabaya for a 1kg package using JNE"

> "Track my package with AWB number JNE1234567890"

> "Show me all cities in DKI Jakarta province"

> "Compare shipping prices from Jakarta to Bandung using JNE, SiCepat, and J&T"

---

## ⚙️ Configuration

<table>
  <thead>
    <tr>
      <th>Environment Variable</th>
      <th>Required</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>RAJAONGKIR_API_KEY</code></td>
      <td align="center">✅</td>
      <td>Your RajaOngkir Komerce API key</td>
    </tr>
    <tr>
      <td><code>RAJAONGKIR_BASE_URL</code></td>
      <td align="center">❌</td>
      <td>API base URL (default: https://rajaongkir.komerce.id/api/v1)</td>
    </tr>
  </tbody>
</table>

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Credits

- [RajaOngkir Komerce](https://rajaongkir.komerce.id) - Shipping API provider
- [Model Context Protocol](https://modelcontextprotocol.io) - MCP specification
