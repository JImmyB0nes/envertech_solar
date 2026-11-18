<p align="center">
  <img src="custom_components/envertech_solar/brand/logo.png" alt="Envertech Solar" width="180">
</p>

<h1 align="center">Envertech Solar for Home Assistant</h1>

<p align="center">
  <strong>Solar yield, power output and station information straight from the Envertech Solar Portal.</strong>
</p>

<p align="center">
  <a href="https://github.com/JImmyB0nes/envertech_solar/releases"><img src="https://img.shields.io/github/v/release/JImmyB0nes/envertech_solar?style=flat&logo=github" alt="Latest release"></a>
  <a href="https://github.com/JImmyB0nes/envertech_solar/stargazers"><img src="https://img.shields.io/github/stars/JImmyB0nes/envertech_solar?style=flat&logo=github" alt="GitHub Stars"></a>
  <a href="https://jimmybones.de/scripts/envertech-cloud"><img src="https://img.shields.io/badge/Forgejo-Mirror-blue?style=flat&logo=gitea&logoColor=white" alt="Forgejo Mirror"></a>
  <a href="https://www.hacs.xyz/"><img src="https://img.shields.io/badge/HACS-Default-41BDF5?logo=homeassistant&logoColor=white" alt="HACS"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="MIT License"></a>
</p>

<p align="center">
  <a href="#-installation">Installation</a> ·
  <a href="#-setup">Setup</a> ·
  <a href="#-sensors">Sensors</a> ·
  <a href="#-help--faq">Help &amp; FAQ</a>
</p>

> **Envertech Solar** connects Home Assistant to the [Envertech Solar Portal](https://www.envertecportal.com/). Enter your station ID once and keep an eye on power, yield and station information.

## ✨ Highlights

- ☀️ **Live solar power** in real time
- 🔋 **Daily, monthly, yearly and total yield**
- ⚡ **Daily peak power** and **all-time peak power**
- 💶 **Feed-in income** and **CO₂ savings**, if configured in the portal
- 🔁 **Adjustable polling interval** directly in Home Assistant
- 🌍 Interface available in English, German, Dutch, Portuguese, Polish, Russian and Chinese
- 🧩 Installable via **HACS**
- 🔌 Built for Envertech ECO-/SE inverters, e.g. 2000SE

## 📦 Installation

### HACS · recommended

[![Open this integration in HACS](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=JImmyB0nes&repository=envertech_solar&category=integration)

1. Open **HACS → Integrations**.
2. Search for **Envertech Solar** and install the integration.
3. Restart Home Assistant.
4. Go to **Settings → Devices & Services → Add Integration**.
5. Search for **Envertech Solar** and enter your station ID.

> 💡 The repository was moved from `jimmybonesde/envertech_solar` to `JImmyB0nes/envertech_solar`. If the default HACS store still points to the old address, add `https://github.com/JImmyB0nes/envertech_solar` under **HACS → ⋮ → Custom repositories** (category: *Integration*).

### Manual

1. Download or clone this repository.
2. Copy `custom_components/envertech_solar` into `config/custom_components/` of your Home Assistant installation.
3. Restart Home Assistant and set up the integration as described above.

## ⚙️ Setup

The integration requires the **station ID** of your system. After setup, you can adjust the polling interval under **⚙️ Configure** (default: 30 seconds; allowed: 10–3,600 seconds).

<details>
<summary><strong>🔍 How do I find my station ID?</strong></summary>

1. Open the [Envertech Solar Portal](https://www.envertecportal.com/terminal/systemoverview).
2. Click on one of your solar panels.
3. The URL contains the value after `/systemhistory/` and before `?sn=`:

```text
https://www.envertecportal.com/terminal/systemhistory/03GFF6E15154525DA16901EC7A4541G1?sn=3014511
                                                     └──────── Station ID ────────┘
```

<img width="400" alt="Selecting a solar panel in the Envertech portal" src="https://github.com/user-attachments/assets/77d86a11-26fe-4db6-a985-79ca1fdd157b" />

</details>

## 📊 Sensors

| Icon | Sensor | Portal value | Unit | Description |
| :--: | --- | --- | :--: | --- |
| ☀️ | Current Power | `Power` | W | Instantaneous solar power |
| ⚡ | Daily Peak Power | `peak_power_today` | W | Highest power measured during the current day |
| 🏆 | All-Time Peak Power | `StrPeakPower` | W | Highest power reported by the portal |
| 📐 | Capacity | `UnitCapacity` | kWp | Installed system capacity |
| 🔋 | Daily Energy | `UnitEToday` | kWh | Energy generated today |
| 🗓️ | Monthly Energy | `UnitEMonth` | kWh | Energy generated this month |
| 📆 | Yearly Energy | `UnitEYear` | kWh | Energy generated this year |
| ♾️ | Total Energy | `UnitETotal` | kWh | Yield since commissioning |
| 🔌 | Inverter Model | `InvModel1` | — | Inverter model reported by the portal |
| 💶 | Income | `StrIncome` | EUR / PLN | Feed-in income, if configured in the portal |
| 🌱 | Carbon Offset | `StrCO2` | t | CO₂ savings calculated by the portal |
| 📍 | Start Date | `CreateTime` | — | Commissioning date of the system |

The energy sensors are especially useful for history charts and the Home Assistant energy dashboard.

## 🖼️ Example

<img width="484" alt="Example Envertech Solar dashboard in Home Assistant" src="https://github.com/user-attachments/assets/4d6787c6-ac72-4726-8753-f7537e0836e3" />

For a clean layout, these cards work well:

- **Gauge cards** for current power
- **Entities cards** for daily, monthly and yearly energy
- **Grid or vertical-stack cards** for a compact station overview

## ❓ Help & FAQ

**The integration does not show up in HACS.**  
Refresh HACS and search for **Envertech Solar** again. The repository must be publicly accessible.

**The station ID is invalid.**  
Make sure you copied exactly the part between `/systemhistory/` and `?sn=` from the portal URL.

**Sensors show `unknown`.**  
Check that the inverter is online and the Envertech Solar Portal is delivering data. Then look for errors in the Home Assistant logs.

**Values update too slowly or too quickly.**  
Adjust the polling interval under **Settings → Devices & Services → Envertech Solar → ⚙️ Configure**.

## 🤝 Contributing

Bug reports and suggestions are welcome:

- 🐛 [Open an issue](https://github.com/JImmyB0nes/envertech_solar/issues)
- 🔀 [Open a pull request](https://github.com/JImmyB0nes/envertech_solar/pulls)
- ⭐ Star the repository if it helps you

## 🙏 Credits & License

Created with ☀️ by **JimmyBones**  
🌐 [JimmyBones.de](https://www.jimmybones.de)

Published under the [MIT License](LICENSE).
