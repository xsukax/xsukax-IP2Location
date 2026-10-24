<div align="center">

# 🌐 xsukax IP2Location

### Find the approximate location behind a public IP address.

**A lightweight, privacy-conscious, single-file IPv4/IPv6 geolocation tool with four free lookup providers, automatic fallback, interactive maps, and shareable JSON views.**

[![License: GPL-3.0](https://img.shields.io/badge/License-GPL--3.0-blue.svg)](LICENSE)
![HTML5](https://img.shields.io/badge/HTML5-Single%20File-E34F26?logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-Vanilla-F7DF1E?logo=javascript&logoColor=black)
![No API Key](https://img.shields.io/badge/API%20Key-Not%20Required-1f883d)
![No Build](https://img.shields.io/badge/Build%20Step-None-6f42c1)

[Features](#-features) · [Quick Start](#-quick-start) · [URL Parameters](#-url-parameters) · [Providers](#-geolocation-providers) · [Privacy](#-privacy-and-accuracy) · [License](#-license)

</div>

---

## 📖 Overview

**xsukax IP2Location** is a responsive, browser-based IP geolocation utility built entirely in a single `index.html` file. Enter any supported **public IPv4 or IPv6 address** to discover its approximate geographic location and available network information, without creating an account, obtaining an API key, installing dependencies, or running an application backend.

The application queries third-party geolocation services directly from your browser and displays the returned information in a clean interface featuring an embedded **OpenStreetMap** map. You can choose a specific lookup provider or let the application automatically try other providers when one fails.

> [!IMPORTANT]
> IP geolocation is **approximate**. It cannot determine an individual's identity or exact physical address. Results depend on third-party databases and can vary between providers.

## ✨ Features

- **Single-file application:** HTML, CSS, and JavaScript are bundled in `index.html`; no frameworks, dependencies, build process, or application server required.
- **IPv4 and IPv6:** Validates addresses and rejects private, reserved, and other non-public address categories recognized by the application.
- **Four keyless providers:** [ipwho.is](https://ipwho.is/), [ipapi.co](https://ipapi.co/), [GeoJS](https://www.geojs.io/), and [FreeIPAPI](https://freeipapi.com/).
- **Automatic provider fallback:** In automatic mode, providers are tried in sequence until one successfully returns usable data.
- **Manual provider selection:** Select a single provider for a lookup without automatic fallback.
- **Map visualization:** Displays approximate coordinates on an embedded [OpenStreetMap](https://www.openstreetmap.org/) map when coordinates are available.
- **Network intelligence:** Displays available city, region, country, postal code, latitude/longitude, ISP, organization, timezone, IP version, and ASN information.
- **Current public IP lookup:** The **Use my IP address** button lets a provider identify your browser's outward-facing IP address.
- **Direct lookup links:** Automatically perform lookups through the `?ip=` URL parameter.
- **JSON view:** Display normalized data alongside the upstream provider's raw JSON response through `?raw=`.
- **Share and copy:** Copy a lookup summary or a link that preserves the selected provider.
- **Provider health checks:** Test all four services against `8.8.8.8` to see which are currently reachable from your browser.
- **Session lookup history:** Revisit up to eight recent addresses; this list is held in page memory and disappears when the page is reloaded.
- **Responsive and accessible:** Mobile-friendly layout, clear feedback messages, keyboard skip link, and reduced-motion support.

## 🚀 Quick Start

### Option 1 — Open the HTML file

1. Download or clone the repository.
2. Open **`index.html`** in a modern web browser.
3. Enter a public IP address, such as `8.8.8.8`, and select **Locate IP**.

```bash
git clone https://github.com/xsukax/xsukax-IP2Location.git
cd xsukax-IP2Location
```

> [!NOTE]
> The app can be opened as a local file, but some browsers restrict cross-origin requests from `file://` pages. For a more reliable experience, serve it over HTTP or HTTPS using either of the following options.

### Option 2 — Run a lightweight local server

If Python 3 is installed:

```bash
cd xsukax-IP2Location
python3 -m http.server 8000
```

Then open **http://localhost:8000/** in your browser.

This Python command is only an optional static-file server. Python is **not** an application dependency.

### Option 3 — Deploy to GitHub Pages

1. Push `index.html`, `README.md`, and `LICENSE` to your GitHub repository.
2. Open the repository's **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select your publishing branch (for example, `main`) and the **`/(root)`** folder, then save.
5. Open the Pages URL shown in GitHub after deployment.

You can also host the same `index.html` file using any HTTPS-enabled static web server or static hosting provider.

## 🧭 How to Use

1. **Enter an address** — type a public IPv4 or IPv6 address, or click **Use my IP address**.
2. **Choose a provider** — keep **Automatic** for fallback support, or choose a specific source.
3. **Locate the IP** — review the approximate geographic location and available network metadata.
4. **Explore the results** — view the map, copy a summary, share a direct link, or select **View JSON**.
5. **Run diagnostics** — use **Test all providers** to check reachability from your browser.

Try these public DNS IP addresses:

```text
8.8.8.8
1.1.1.1
2001:4860:4860::8888
```

## 🔗 URL Parameters

The app supports direct links, so a static deployment can be used without manually entering an address.

| Parameter | Description | Example |
| --- | --- | --- |
| `ip` | Automatically look up an IP and show the graphical result. | `?ip=8.8.8.8` |
| `raw` | Automatically look up an IP and display a JSON document in the browser. | `?raw=8.8.8.8` |
| `provider` | Select a provider for either view. Omit or set to `auto` for automatic fallback. | `?ip=8.8.8.8&provider=geojs` |

### Examples

```text
# Interactive location + map
index.html?ip=8.8.8.8

# IPv6 lookup
index.html?ip=2001:4860:4860::8888

# JSON view, with automatic fallback
index.html?raw=8.8.8.8

# Interactive lookup using only GeoJS
index.html?ip=8.8.8.8&provider=geojs

# JSON view using only ipapi.co
index.html?raw=1.1.1.1&provider=ipapico

# JSON view using only FreeIPAPI
index.html?raw=8.8.8.8&provider=freeipapi
```

Supported provider identifiers:

| Identifier | Source |
| --- | --- |
| `auto` | Automatic fallback (default) |
| `ipwhois` | ipwho.is |
| `ipapico` | ipapi.co |
| `geojs` | GeoJS |
| `freeipapi` | FreeIPAPI |

Domain-style aliases such as `ipwho.is`, `ipapi.co`, `geojs.io`, and `freeipapi.com` are also accepted. If both `raw` and `ip` are supplied, **`raw` takes precedence**.

> [!WARNING]
> **`?raw=` is a browser-rendered JSON view, not a conventional HTTP JSON API endpoint.** This static HTML application initially returns HTML and then uses JavaScript to fetch and display JSON. It does **not** return an `application/json` response suitable for a normal `curl` request or server-side API integration. For a machine-to-machine API, query the underlying providers directly or build a separate server-side endpoint.

## 🌍 Geolocation Providers

Each provider is accessed directly over HTTPS without a configured API key.

| Priority in automatic mode | Provider | Identifier | Website |
| --- | --- | --- | --- |
| 1 | ipwho.is | `ipwhois` | https://ipwho.is/ |
| 2 | ipapi.co | `ipapico` | https://ipapi.co/ |
| 3 | GeoJS | `geojs` | https://www.geojs.io/ |
| 4 | FreeIPAPI | `freeipapi` | https://freeipapi.com/ |

**Automatic mode** tries the sources in the listed order; a failed, timed-out, blocked, or unusable response triggers the next provider. **Manual mode** queries only the selected service.

The application uses a **7.5-second timeout per provider** and normalizes differing API response formats into a consistent display. Field availability varies by source; a field that a provider does not return is shown as unavailable rather than invented.

Provider availability, rate limits, usage conditions, response fields, and browser CORS policies are controlled by the upstream services and may change over time.

## 📦 Project Structure

```text
xsukax-IP2Location/
├── index.html     # Complete HTML, CSS, and JavaScript application
├── README.md      # Project documentation
└── LICENSE        # GNU General Public License, version 3
```

## ⚙️ Technical Details

| Component | Implementation |
| --- | --- |
| Frontend | Semantic HTML5, embedded CSS3, vanilla JavaScript |
| Hosting | Static files; no application backend required |
| Data retrieval | Browser `fetch()` requests to third-party HTTPS APIs |
| Provider selection | URL parameter or on-page dropdown |
| Error handling | Input validation, per-source timeout, provider fallback, and clear error messages |
| Mapping | Embedded OpenStreetMap iframe |
| Lookup history | In-memory JavaScript array (last 8 successful results) |
| JSON mode | Browser-rendered, formatted JSON with normalized and upstream data |
| Configuration | Provider definitions and `PROVIDER_TIMEOUT_MS` inside `index.html` |

No external JavaScript frameworks or CSS libraries are loaded by the application itself. Internet access is required to reach the lookup providers and display the online map.

## 🔒 Privacy and Accuracy

This is a **client-side application**, not a private/offline geolocation database.

- **Third-party requests:** Public IP addresses being looked up are sent from your browser to the selected geolocation provider. Automatic mode may contact more than one service when fallback is needed.
- **Map requests:** If location coordinates are available, an OpenStreetMap iframe is loaded and makes requests to that external service.
- **No application-side account or database:** The provided HTML contains no account registration, custom tracking backend, or persistent lookup-history storage. The site hosting the file and external services may have their own logging and privacy policies.
- **Session-only history:** The recent-address list exists only in browser memory and can be cleared using the provided button or by reloading the page.
- **Approximate results:** Geolocation may reflect ISP infrastructure, provider records, a VPN exit node, proxy, or mobile carrier gateway rather than a user's physical location.
- **Provider variation:** Locations, coordinates, timezones, and network labels can differ between sources. Some information may be unavailable or out of date.

Do not use geolocation results as definitive evidence of a person's location, identity, residence, or device position.

## 🛠️ Troubleshooting

| Issue | What to try |
| --- | --- |
| Lookup fails for every provider | Confirm your internet connection, serve the file over HTTP/HTTPS, and select **Test all providers**. |
| A provider returns a network or CORS error | Try **Automatic** mode or another provider. Its endpoint or browser access policy may have changed. |
| An address is rejected | Confirm that the address is a correctly formatted **public** IPv4 or IPv6 address. Private and reserved ranges are not geolocated. |
| Some network fields are blank | The selected provider may not supply that data. Try another source. |
| Map does not appear | The provider may not have returned valid coordinates, or OpenStreetMap may be unavailable or blocked. |
| JSON URL does not work with `curl` | The page displays JSON using JavaScript; it is not an HTTP JSON API. |
| Copy link/summary fails | Use a modern browser and try serving the page from HTTPS or `localhost` if clipboard permissions are restricted. |

## 🤝 Contributing

Contributions, bug reports, and feature suggestions are welcome.

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/your-feature`.
3. Make and test your changes in modern desktop and mobile browsers.
4. Commit your changes and open a pull request with a concise explanation.

Please keep the core project lightweight, accessible, and easy to deploy as a single HTML file.

[Open an issue](https://github.com/xsukax/xsukax-IP2Location/issues) · [View the repository](https://github.com/xsukax/xsukax-IP2Location)

## 📜 License

Copyright © 2026 **xsukax**.

This project is distributed under the **GNU General Public License, version 3.0 (`GPL-3.0-only`)**. You may use, study, modify, and redistribute it under the terms of that license. See [LICENSE](LICENSE) for the complete license text.

---

<div align="center">

**xsukax IP2Location** — Simple IP intelligence. No installation. No API key.

Made available as open-source software by [@xsukax](https://github.com/xsukax).

</div>
