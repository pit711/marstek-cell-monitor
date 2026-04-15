# Marstek Venus E – Cell Monitor

Single-file HTML dashboard for live monitoring of all 16 cell voltages of a **Marstek Venus E** LiFePO4 battery via **Home Assistant**. No build step, no server, no cloud – just open the HTML file in a browser.

## Disclaimer

This project is not affiliated with, endorsed by, or associated with Marstek Energy Technology. Marstek and Venus are trademarks of their respective owners. Home Assistant is a trademark of Nabu Casa, Inc. This is an independent community project for interoperability purposes.

Bilingual UI: **Deutsch / English** (switchable in the setup wizard and in the dashboard header).

![dashboard](https://img.shields.io/badge/single--file-HTML-blue) ![deps-none](https://img.shields.io/badge/deps-Chart.js%20CDN-lightgrey) ![license](https://img.shields.io/badge/license-MIT-green)

## Features

- Live view of all 16 individual cell voltages (WebSocket subscription to HA)
- Pack voltage, average, min/max, delta, standard deviation
- 24 h history of min / max / avg and delta (via HA recorder statistics)
- Pack health score with color-coded rating
- Detail table per cell with deviation from mean
- LiFePO4 threshold reference table
- **DE / EN language toggle** (stored in localStorage)
- Token + URL stored **only** in browser localStorage – no third-party calls, works fully offline after first load (Chart.js is loaded once from jsDelivr)

## Requirements

1. **Marstek Venus E** (v1/v2 or v3)
2. Modbus TCP connection to the battery:
   - **Venus E v3:** directly via Ethernet cable at the LAN port (no adapter needed)
   - **Venus E v1/v2:** RS485-to-WiFi/Ethernet gateway (e.g. Elfin EW11, PUSR DR134, Waveshare RS485-RJ45) at the RS485 port
3. **Home Assistant Core 2025.9** or newer
4. The [Marstek Venus Modbus plugin](https://github.com/ViperRNMC/marstek_venus_modbus) installed via HACS and configured
5. The 16 cell sensors enabled in HA (they are disabled by default)

## Enable the cell sensors in HA

1. HA → Settings → Devices & Services → *Marstek Venus Modbus* → Entities
2. Search for `zelle` – you will find 16 disabled sensors
3. Enable all of them (multi-select supported)
4. Plugin options → set *Low Priority* polling interval to **300 s**

## Long-Lived Access Token

1. HA → click your profile (bottom left)
2. Tab *Security* → *Long-lived access tokens* → *Create token*
3. Copy the token (shown only once!)

## Usage

1. Download `marstek-zellen-monitor.html`
2. Open it in any modern browser (Chrome, Firefox, Edge, Safari)
3. On first launch the setup wizard appears – pick language, enter HA URL + token, click *Connect & Save*
4. Done. The dashboard reconnects automatically on page reload or network drops.

The configuration is stored in `localStorage` under the keys `marstek_zellen_config` and `marstek_zellen_lang`. Click **⚙ Setup** in the header to reset.

## Sensor prefix

Default: `sensor.marstek_venus_modbus_batteriepack_1_zelle_`

The dashboard expects 16 sensors matching `{prefix}{1..16}_spannung`. If your HA instance exposes them under a different name, adjust the prefix field in the wizard.

## Privacy

- Token and URL are stored **exclusively** in your browser's localStorage
- No telemetry, no analytics, no external servers beyond the Chart.js CDN
- The file can be self-hosted or used fully offline (just vendor Chart.js locally)

**Note:** Chart.js is loaded once from cdn.jsdelivr.net. Your IP address may be disclosed to this CDN provider. For full GDPR compliance, you can download Chart.js and host it locally.

**Security Note:** Your Home Assistant access token is stored in your browser's localStorage (unencrypted). Only use this tool in a trusted, private browser context. Consider using sessionStorage or clearing localStorage when done.

## Screenshots

Setup wizard and dashboard run in any modern browser – no installation required.

## License

MIT
