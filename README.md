# What Is My IP? — Public IPv4 & IPv6 Checker

A modern, high-performance, single-file web application to check and display your public IPv4 and IPv6 addresses. It reflects your connection stack in real-time, displays status indicators, copies addresses with a single click, and enriches the results with network and geographic details (ISP, ASN, Location, and Timezone).

---

## 🚀 Live Demo & Hosting
Since this utility is entirely client-side and self-contained, you can run it:
1. **Locally:** Simply download [index.html](file:///e:/myip/index.html) and open it directly in any modern web browser.
2. **Static Hosting:** Drop [index.html](file:///e:/myip/index.html) onto static hosting services like GitHub Pages, Netlify, Vercel, Cloudflare Pages, or AWS S3.

---

## ✨ Features

- **Dual-Stack IP Detection:** Simultaneously queries IPv4 and IPv6 endpoints asynchronously using a resilient multi-endpoint fallback chain.
- **Ad-Blocker Resilient:** Multiple fallback endpoints are tried in sequence — if a privacy filter blocks one provider, the next is tried automatically with no user interaction required.
- **Connection Status Indicators:** Clear visual states for both stacks:
  - 🟢 **Connected:** Successful IP detection.
  - 🟡 **Checking:** Resolution in progress.
  - 🔴 **Not Available / Failed:** No network support or all endpoints failed (ideal for verifying if your network/VPN lacks IPv6).
- **Geo-Location & ISP Enrichment:** Automatically fetches network details on success using the `ipwho.is` API:
  - Internet Service Provider (ISP) and Autonomous System Number (ASN).
  - Geographic location (City, Region, Country with flag emoji).
  - Timezone details.
- **Modern Premium Design:**
  - Radial gradient backgrounds, dark theme, and high-quality colors.
  - Glassmorphic panels with subtle micro-animations (loading spinners, hover effects).
  - Fully responsive grid layout optimized for mobile, tablet, and desktop screens.
  - Embedded high-resolution vector (SVG) favicon assets.
- **Quick Copying:** Quick copy button with feedback transitions and automatic clipboard API fallback support.
- **Self-Contained & Lightweight:** No build step, no npm modules, and no external CSS/JS framework dependencies. Under 35KB in total.

---

## 🛠️ How It Works

The app operates strictly client-side using Vanilla JS:
1. **Resilient Fallback Chain:** The browser tries multiple public API endpoints in priority order for each protocol. If any endpoint is blocked (e.g., by an ad blocker, privacy filter, or network policy), the next is tried silently and automatically:
   - **IPv4 endpoints (in order):**
     1. `https://api4.ipify.org?format=json` — JSON response
     2. `https://v4.ident.me` — Plain text, CORS enabled
     3. `https://ipv4.icanhazip.com` — Plain text, Cloudflare-powered, CORS enabled
   - **IPv6 endpoints (in order):**
     1. `https://v6.ident.me` — Plain text, CORS enabled
     2. `https://ipv6.icanhazip.com` — Plain text, Cloudflare-powered, CORS enabled
     3. `https://api6.ipify.org?format=json` — JSON response (tried last as it is frequently blocked by EasyPrivacy/Brave Shields)
2. **Aborting Hangs:** Utilizes the `AbortController` API with a `9.0 second` timeout per endpoint to prevent infinite hangs.
3. **ISP & Location Enrichment:** Upon obtaining the IP address, a request is fired to `https://ipwho.is/<ip>` to dynamically populate detailed metadata tables.
4. **Clipboard Copying:** Uses the modern asynchronous `navigator.clipboard` API with a fallback to a dynamically generated `<textarea>` element for older browsers.

---

## 📂 Project Structure

The project layout is as simple as it gets:
```
myip/
├── index.html   # Main self-contained HTML/CSS/JS application
└── README.md    # Documentation and usage guide
```

---

## 🌐 API Credits

Special thanks to the free public services powering this tool:
- [ipify](https://www.ipify.org/) — Fast IP address reflection (IPv4 and IPv6).
- [ident.me](https://api.ident.me/) — Lightweight dual-stack IP reflection with CORS support.
- [icanhazip.com](https://icanhazip.com/) — Cloudflare-powered dual-stack IP reflection with CORS support.
- [ipwhois](https://ipwho.is/) — Geography and ASN resolution.
