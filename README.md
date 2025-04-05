# Home media server Docker setup
A complete Docker Compose setup for a self-hosted home media server with automated downloading, organization, and 
streaming capabilities.

## Features
- **Media Management**: Plex for media streaming, with Sonarr (TV) and Radarr (Movies) for automated downloading
- **VPN Integration**: NordLynx (WireGuard) for secure torrenting with qBittorrent
- **Subtitle Support**: Bazarr for automated subtitle downloading
- **Indexers**: Jackett and Prowlarr for torrent index management
- **Remote Access**: WireGuard VPN and DuckDNS for dynamic DNS
- **Auto-healing**: Automatic container monitoring and restart
- **Mobile Streaming**: Stremio for mobile viewing

## Prerequisites
1. Docker and Docker Compose installed
2. Basic understanding of Docker concepts
3. A DuckDNS account (for dynamic DNS)
4. A NordVPN account (for NordLynx)

## Setup instructions
1. Clone this repository:
   ```bash
   git clone https://github.com/danozka/home-media-server.git
   cd home-media-server
   ```
   
2. Create a `.env` file by copying the example:
   ```bash
   cp .env.example .env
   ```

3. Edit the `.env` file with your specific configuration:
    ```bash
   nano .env
   ```

4. Start the services:
    ```bash
   docker compose up -d
   ```
