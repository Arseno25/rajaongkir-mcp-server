# RajaOngkir MCP Server

<p align="center">
  <a href="README.md">🇬🇧 English</a> •
  <a href="README.id.md">🇮🇩 Bahasa Indonesia</a>
</p>

A lightweight [Model Context Protocol (MCP)](https://modelcontextprotocol.io) server that enables AI assistants like Claude and Cursor to calculate Indonesian shipping costs and track packages via RajaOngkir API.

- [Example Interactions](#example-interactions)
- [Tools](#tools)
  - [Location Search](#location-search)
  - [Hierarchical Location](#hierarchical-location)
  - [Cost Calculation](#cost-calculation)
  - [Package Tracking](#package-tracking)
- [Setup](#setup)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Configuration](#configuration)
- [Integrating with Claude Desktop and Cursor](#integrating-with-claude-desktop-and-cursor)

## Example Interactions

- "Calculate shipping cost from Jakarta to Surabaya for a 1kg package"
- "Compare JNE, SiCepat, and J&T prices from Bandung to Yogyakarta"
- "Track my package with AWB number JNE1234567890"
- "Show me all districts in Jakarta Pusat"

## Tools

### Location Search

1. **searchDomesticDestination**
   - Description: Search for cities/districts in Indonesia
   - Parameters:
     - `query` (string): The location name to search
   - Returns: List of matching locations with IDs
   - Example: `searchDomesticDestination("Jakarta")`

2. **searchInternationalDestination**
   - Description: Search for international countries
   - Parameters:
     - `query` (string): The country name to search
   - Returns: List of matching countries with IDs
   - Example: `searchInternationalDestination("Singapore")`

### Hierarchical Location

3. **getProvinces**
   - Description: Get all Indonesian provinces
   - Parameters: None
   - Returns: List of provinces with IDs
   - Example: `getProvinces()`

4. **getCities**
   - Description: Get cities within a province
   - Parameters:
     - `province_id` (string): The province ID
   - Returns: List of cities with IDs
   - Example: `getCities("6")` (DKI Jakarta)

5. **getDistricts**
   - Description: Get districts within a city
   - Parameters:
     - `city_id` (string): The city ID
   - Returns: List of districts with IDs
   - Example: `getDistricts("152")` (Jakarta Pusat)

6. **getSubdistricts**
   - Description: Get subdistricts within a district
   - Parameters:
     - `district_id` (string): The district ID
   - Returns: List of subdistricts with IDs
   - Example: `getSubdistricts("2096")`

### Cost Calculation

7. **calculateDomesticCost**
   - Description: Calculate domestic shipping cost using location IDs from search
   - Parameters:
     - `origin` (string): Origin location ID
     - `destination` (string): Destination location ID
     - `weight` (int): Package weight in grams
     - `courier` (string): Courier code (jne, sicepat, jnt, pos, tiki, etc)
   - Returns: Shipping cost options
   - Example: `calculateDomesticCost("12345", "67890", 1000, "jne")`

8. **calculateDistrictCost**
   - Description: Calculate shipping cost using district IDs (supports multiple couriers)
   - Parameters:
     - `origin` (string): Origin district ID
     - `destination` (string): Destination district ID
     - `weight` (int): Package weight in grams
     - `courier` (string): Courier codes separated by colon
   - Returns: Shipping cost options from all specified couriers
   - Example: `calculateDistrictCost("1391", "1376", 1000, "jne:sicepat:jnt")`

9. **calculateInternationalCost**
   - Description: Calculate international shipping cost
   - Parameters:
     - `origin` (string): Origin location ID (Indonesia)
     - `destination` (string): Destination country ID
     - `weight` (int): Package weight in grams
     - `courier` (string): Courier code (pos, jne, tiki, ems)
   - Returns: International shipping cost options
   - Example: `calculateInternationalCost("12345", "108", 1000, "pos")`

### Package Tracking

10. **trackPackage**
    - Description: Track package by AWB/tracking number
    - Parameters:
      - `awb` (string): Tracking number
      - `courier` (string): Courier code
    - Returns: Tracking status and shipment history
    - Example: `trackPackage("JNE1234567890", "jne")`

## Setup

### Prerequisites

- Python 3.10+
- RajaOngkir Komerce API Key

### Installation

```bash
git clone https://github.com/Arseno25/rajaongkir-mcp-server.git
cd rajaongkir-mcp-server
pip install -r requirements.txt
```

### Configuration

Create a `.env` file in the project root (you can copy and modify the provided example):

```bash
cp .env.example .env
```

Then edit the file with your API key:

```env
RAJAONGKIR_API_KEY=your-api-key-here
RAJAONGKIR_BASE_URL=https://rajaongkir.komerce.id/api/v1
```

### Getting a RajaOngkir API Key

1. Go to [RajaOngkir Komerce](https://rajaongkir.komerce.id)
2. Create an account or log in
3. Subscribe to a plan (free tier available)
4. Copy your API key from the dashboard

## Integrating with Claude Desktop and Cursor

To use this MCP server with Claude Desktop, add it to your Claude configuration (`claude_desktop_config.json`):

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

For Cursor, go to the MCP tab in Cursor Settings. Add a server with this command:

```
python path/to/rajaongkir-mcp-server/server.py
```

### Supported Couriers

**Domestic:** JNE, SiCepat, J&T, POS Indonesia, TIKI, AnterAja, Ninja Xpress, Lion Parcel, ID Express, SAP, NCS, REX, RPX, Wahana, and more.

**International:** POS Indonesia, JNE, TIKI, EMS

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
