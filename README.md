# Harmonia

<div align="center">

**A fast, modern, and open-source desktop music player inspired by Spotify.**  
Built with **Tauri v2**, **React 19**, **TypeScript**, and **Tailwind CSS**. Powered by the **Subsonic & Navidrome** standard.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Tauri v2](https://img.shields.io/badge/Tauri-v2-24C8DB?logo=tauri&logoColor=white)](https://tauri.app)
[![React 19](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=black)](https://react.dev)
[![Tailwind CSS v4](https://img.shields.io/badge/Tailwind_CSS-v4-38B2AC?logo=tailwind-css&logoColor=white)](https://tailwindcss.com)
[![Navidrome Compatible](https://img.shields.io/badge/Compatible-Navidrome_%2F_Subsonic-00B4D8)](https://www.navidrome.org)

</div>

---

## ✨ Features

- 🎧 **Spotify-inspired UX:** Dark sleek theme, responsive sidebar, navigation history, and persistent bottom player.
- ⚡ **Ultra-lightweight:** Consumes **~35 MB of RAM** and weighs ~12 MB (unlike traditional 500 MB Electron apps).
- 🌐 **Subsonic / Navidrome Standard:** Seamlessly connects to any Subsonic-compatible server (Navidrome, Jellyfin, Airsonic) with full streaming support.
- 🐳 **Docker-ready Backend:** Includes a 1-command Docker Compose setup to host your personal music library in seconds.
- 🚀 **Offline & Demo Mode:** Works out of the box with royalty-free tracks for testing without requiring a server setup.
- 🛡️ **Zero Telemetry & 100% Free:** No tracking, no ads, no cloud vendor lock-in.

---

## 🏗️ Architecture

```mermaid
flowchart LR
    subgraph Client ["Harmonia Desktop (Tauri)"]
        UI["React 19 + Tailwind CSS"]
        State["Zustand Store (Audio & Queue)"]
        SubsonicClient["Subsonic REST API Client (MD5 Auth)"]
        TauriCore["Tauri Core (Rust / WebView2)"]
        
        UI <--> State
        State <--> SubsonicClient
        UI <--> TauriCore
    end

    subgraph Server ["Personal Cloud / Local Server"]
        Navidrome["Navidrome Server (Docker)"]
        MusicStorage[("Music Folder (.mp3, .flac)")]
        Navidrome <--> MusicStorage
    end

    SubsonicClient <-->|REST API + HTTP Range Streaming| Navidrome
```

---

## 🚀 Quick Start

### 1. Run the Desktop Client

Clone the repository and install dependencies:

```bash
# Install dependencies
npm install

# Run in Web Mode (Fast browser development with Hot Reload)
npm run dev

# Run in Desktop Mode (Native Windows executable with Tauri)
npm run tauri dev
```

### 2. Launch your Personal Music Server (Navidrome with Docker)

Place your music files (`.mp3`, `.flac`, `.m4a`) in `docker/music/`, then start the server:

```bash
cd docker
docker compose up -d
```

1. Open **http://localhost:4533** in your browser to create your initial admin account.
2. In **Harmonia**, click **Configurar Servidor** (top right) and enter your server URL and credentials.

---

## 📦 Building for Production

To compile the standalone Windows executable (`.exe`) and installer (`.msi`):

```bash
npm run tauri build
```

---

## 📄 License

This project is open-source under the [MIT License](LICENSE).
# Carlos-jim
