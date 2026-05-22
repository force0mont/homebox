# Homebox

> A fork of [sysadminsmedia/homebox](https://github.com/sysadminsmedia/homebox) — Home inventory and organization system.

[![Go Version](https://img.shields.io/badge/go-1.21+-blue.svg)](https://golang.org/)
[![License](https://img.shields.io/badge/license-AGPL--3.0-green.svg)](LICENSE)

## Overview

Homebox is a self-hosted home inventory and organization system built for the home user. It allows you to track your belongings, manage locations, and keep notes on items in your home.

> **Personal fork notes:** I'm running this on a Raspberry Pi 4 with a 32 GB SD card. I've bumped the default max upload size to 25 MB to better handle photos taken on modern smartphones. I've also disabled open registration by default since this is a single-household instance.

## Features

- 📦 Track items across multiple locations
- 🏷️ Label and categorize your belongings
- 🔍 Full-text search across all items
- 📸 Attach photos and documents to items
- 📊 Warranty and purchase tracking
- 🔒 Multi-user support with authentication
- 🐳 Docker-first deployment

## Getting Started

### Prerequisites

- [Go 1.21+](https://golang.org/dl/)
- [Node.js 18+](https://nodejs.org/)
- [Docker](https://www.docker.com/) (optional, recommended for production)

### Development Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/your-org/homebox.git
   cd homebox
   ```

2. **Using Dev Container (recommended)**

   Open in VS Code and select "Reopen in Container" when prompted.

3. **Manual setup**

   ```bash
   # Install backend dependencies
   cd backend
   go mod download

   # Install frontend dependencies
   cd ../frontend
   npm install
   ```

4. **Run in development mode**

   ```bash
   # Start backend
   cd backend
   go run ./app/api/main.go

   # Start frontend (separate terminal)
   cd frontend
   npm run dev
   ```

### Docker Deployment

```yaml
version: '3.8'
services:
  homebox:
    image: ghcr.io/your-org/homebox:latest
    ports:
      - "7745:7745"
    volumes:
      - homebox-data:/data
    environment:
      - HBOX_LOG_LEVEL=info
      - HBOX_LOG_FORMAT=text
      - HBOX_WEB_MAX_UPLOAD_SIZE=25
      - HBOX_OPTIONS_ALLOW_REGISTRATION=false
volumes:
  homebox-data:
```

## Configuration

Homebox is configured via environment variables:

| Variable | Default | Description |
|---|---|---|
| `HBOX_LOG_LEVEL` | `info` | Log level (debug, info, warn, error) |
| `HBOX_LOG_FORMAT` | `text` | Log format (text, json) |
| `HBOX_WEB_PORT` | `7745` | HTTP port to listen on |
| `HBOX_WEB_HOST` | `` | Host to bind to |
| `HBOX_WEB_MAX_UPLOAD_SIZE` | `25` | Max upload size in MB (increased from upstream default of 10) |
| `HBOX_STORAGE_DATA` | `./data` | Path to data directory |
| `HBOX_OPTIONS_ALLOW_REGISTRATION` | `false` | Allow new user registration (set to `true` if you need to add users) |

## Contributing

Contributions are welcome! Please read our [contributing guidelines](.github/AGENTS.md) before submitting a pull request.

1. Fork the repository
2. Create a feature branch (`git checkout -b feat/amazing-feature`)
3. Commit your changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git pu