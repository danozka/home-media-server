# Your all-in-one home media server solution (self-hosted Netflix alternative)
**Tired of juggling multiple streaming subscriptions?** Frustrated with content disappearing from platforms? Want 
complete control over your media without the hassle? This Docker setup is your answer to **cutting the cord for good** 
while enjoying automated, organized media bliss.

* [Why you will love this setup](#why-you-will-love-this-setup)
* [Quick start](#quick-start)
* [Key features](#key-features)
* [Pro tips for maximum enjoyment](#pro-tips-for-maximum-enjoyment)
* [Environment variables](#environment-variables)
* [Accessing services](#accessing-services)
* [Configuring services](#configuring-services)
* [Maintenance](#maintenance)
* [Security notes](#security-notes)
* [Troubleshooting](#troubleshooting)
* [Contribute & customize](#contribute--customize)

## Why you will love this setup
- ### Stream like a pro without headaches
  - **Never manually download again**: Auto-magic fetching of TV shows (Sonarr) and movies (Radarr) the moment they are 
  available
  - **Instant gratification**: Watch torrents *immediately* with Stremio while they download (no more waiting!)
  - **No more "subtitle not found"**: Bazarr automatically grabs subtitles so you are never left squinting

- ### Torrent safely without ISP warnings
  - Built-in WireGuard VPN tunnels all torrent traffic through qBittorrent
  - Your IP stays hidden while you build your media library
  - Sleep easy knowing your activity is private

- ### Access your media anywhere
  - Secure remote access via WireGuard VPN (set up in minutes)
  - Dynamic DNS (DuckDNS) keeps you connected even if your home IP changes
  - Plex organizes everything with beautiful metadata - browse like Netflix but own your content

## Quick start
**Prerequisites**:
- Git and Docker Compose installed
- DuckDNS account (for dynamic DNS)
- NordVPN subscription (for secure VPN connection)

**You do not need to be a Docker expert** - if you can edit a config file, you can have this running today:

```bash
git clone https://github.com/danozka/home-media-server.git
cd home-media-server
cp .env.example .env
nano .env  # Fill in your details
docker compose up -d
```

- Check [Environment variables](#environment-variables) section to know what settings you can tweak
- Check [Accessing services](#accessing-services) section to know how to access each service
- Check [Configuring services](#configuring-services) section to know how to fine-tune each service

## Key features
|         Feature          |                                 Benefit                                 |
|:------------------------:|:-----------------------------------------------------------------------:|
|   **Auto-downloading**   |    New episodes appear magically like they do on streaming services     |
|  **Instant streaming**   |            Start watching torrents immediately with Stremio             |
| **Bulletproof privacy**  |                 VPN-protected torrenting built right in                 |
|     **Self-healing**     |        Containers automatically restart if something goes wrong         |
| **All-in-one dashboard** |             Manage everything through clean web interfaces              |

## Pro tips for maximum enjoyment
1. **Mobile access**: Scan the WireGuard QR code to take your media on the go
2. **Quality control**: Set preferred download resolutions in Sonarr / Radarr
3. **Storage smarts**: Keep seeding while watching with hard links
   
## Environment variables
|           Variable            |                                              Description                                              |                  Example                  |
|:-----------------------------:|:-----------------------------------------------------------------------------------------------------:|:-----------------------------------------:|
|      `MEDIA_SERVER_NAME`      |                                      Name for your media server                                       |             `my-media-server`             |
|           `USER_ID`           |                                     User ID for file permissions                                      |                  `1000`                   |
|          `GROUP_ID`           |                                     Group ID for file permissions                                     |                  `1000`                   |
|          `TIME_ZONE`          | Your time zone (check this [list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List)) |              `Europe/London`              |
|       `MEDIA_SERVER_IP`       |                                        Your server's local IP                                         |              `192.168.1.34`               |
|  `MEDIA_SERVER_NETWORK_CIDR`  |                                        Your local network CIDR                                        |             `192.168.1.0/24`              |
|      `DUCKDNS_SUBDOMAIN`      |                                        Your DuckDNS subdomain                                         |                `my-server`                |
|        `DUCKDNS_TOKEN`        |                                          Your DuckDNS token                                           |         `my-secret-duckdns-token`         |
|       `VPN_PRIVATE_KEY`       |                                            VPN private key                                            |           `my-vpn-private-key`            |
|  `MEDIA_SERVER_CONFIG_PATH`   |                                         Path for config files                                         |            `/path/to/configs`             |
|  `MEDIA_SERVER_MOVIES_PATH`   |                                            Path for movies                                            |             `/path/to/movies`             |
|    `MEDIA_SERVER_TV_PATH`     |                                           Path for TV shows                                           |               `/path/to/tv`               |
| `MEDIA_SERVER_DOWNLOADS_PATH` |                                          Path for downloads                                           |           `/path/to/downloads`            |
|      `STREMIO_HOSTNAME`       |                                         Hostname for Stremio                                          | `192-168-1-34.519b6502d940.stremio.rocks` |
|         `BAZARR_PORT`         |                                         Port to access Bazarr                                         |                  `6767`                   |
|        `JACKETT_PORT`         |                                        Port to access Jackett                                         |                  `9117`                   |
|        `PROWLARR_PORT`        |                                        Port to access Prowlarr                                        |                  `9696`                   |
|   `QBITTORRENT_WEBUI_PORT`    |                                   Port to access qBittorrent Web UI                                   |                  `8090`                   |
|         `RADARR_PORT`         |                                         Port to access Radarr                                         |                  `7878`                   |
|         `SONARR_PORT`         |                                         Port to access Sonarr                                         |                  `8989`                   |
|     `STREMIO_SERVER_PORT`     |                                     Port to access Stremio server                                     |                  `12470`                  |
|     `STREMIO_WEBUI_PORT`      |                                     Port to access Stremio Web UI                                     |                  `8080`                   |
|       `WIREGUARD_PORT`        |                                    Port for WireGuard connections                                     |                  `51820`                  |

## Accessing services
After starting, you can access the services at (using the values from [.env.example](./.env.example)):

|   Service   | Port  |                          URL                           |
|:-----------:|:-----:|:------------------------------------------------------:|
|    Plex     | 32400 |            `http://192.168.1.34:32400/web`             |
|   Sonarr    | 8989  |               `http://192.168.1.34:8989`               |
|   Radarr    | 7878  |               `http://192.168.1.34:7878`               |
|   Bazarr    | 6767  |               `http://192.168.1.34:6767`               |
| qBittorrent | 8090  |               `http://192.168.1.34:8090`               |
|   Jackett   | 9117  |               `http://192.168.1.34:9117`               |
|  Prowlarr   | 9696  |               `http://192.168.1.34:9696`               |
|   Stremio   | 8080  | `https://192-168-1-34.519b6502d940.stremio.rocks:8080` |
|  WireGuard  | 51820 |              UDP port for VPN connections              |

## Configuring services
1. **Plex**: Complete the initial setup wizard and add your media libraries
2. **Sonarr / Radarr**: Configure indexers (Jackett / Prowlarr) and download client (qBittorrent)
3. **Bazarr**: Configure subtitle providers
4. **qBittorrent**: Set network interface to the VPN one and configure appropriate ports
5. **WireGuard**: Scan the QR codes in `/config/wireguard/peerX` to connect mobile devices
6. **Stremio**: Set streaming server port to `https://192-168-1-34.519b6502d940.stremio.rocks:12470/`

## Maintenance
- **Updates**: Run `docker compose pull && docker compose up -d` to update all containers
- **Backups**: Regularly back up your config directories
- **Monitoring**: The auto-heal service will automatically restart unhealthy containers

## Security notes
1. Change default credentials for all services
2. Consider setting up authentication reverse proxy for web interfaces
3. Regularly update your containers and host system
4. Only expose necessary ports to the Internet

## Troubleshooting
Check container logs with:
```bash
docker compose logs <service-name>
```

## Contribute & customize
PRs welcome! Licensed under [MIT](./LICENSE).
