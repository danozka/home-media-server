# Home media server Docker setup
A complete Docker Compose setup for a self-hosted home media server with automated downloading, organization, and 
streaming capabilities.

## Features
- **Media management**: Plex for media streaming, with Sonarr (TV) and Radarr (movies) for automated downloading
- **VPN integration**: NordLynx (WireGuard) for secure torrenting with qBittorrent
- **Subtitle support**: Bazarr for automated subtitle downloading
- **Indexers**: Jackett and Prowlarr for torrent index management
- **Remote access**: WireGuard VPN and DuckDNS for dynamic DNS
- **Auto-healing**: Automatic container monitoring and restart
- **Instant streaming**: Stremio for on-demand viewing of torrents (no pre-download required)

## Prerequisites
1. Docker and Docker Compose installed
2. Basic understanding of Docker concepts
3. A DuckDNS account (for dynamic DNS)
4. A NordVPN subscription (for NordLynx)

## Setup Instructions
1. Clone this repository:
   ```bash
   git clone https://github.com/danozka/home-media-server.git
   cd home-media-server
   ```
2. Create a `.env` file by copying the example [.env.example](./.env.example):
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
   
### Required environment variables
|           Variable            | Description                                                                                           |                  Example                  |
|:-----------------------------:|:------------------------------------------------------------------------------------------------------|:-----------------------------------------:|
|      `MEDIA_SERVER_NAME`      | Name for your media server                                                                            |             `my-media-server`             |
|           `USER_ID`           | User ID for file permissions                                                                          |                  `1000`                   |
|          `GROUP_ID`           | Group ID for file permissions                                                                         |                  `1000`                   |
|          `TIME_ZONE`          | Your time zone (check this [list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List)) |              `Europe/London`              |
|       `MEDIA_SERVER_IP`       | Your server's local IP                                                                                |              `192.168.1.34`               |
|  `MEDIA_SERVER_NETWORK_CIDR`  | Your local network CIDR                                                                               |             `192.168.1.0/24`              |
|      `DUCKDNS_SUBDOMAIN`      | Your DuckDNS subdomain                                                                                |                `my-server`                |
|        `DUCKDNS_TOKEN`        | Your DuckDNS token                                                                                    |         `my-secret-duckdns-token`         |
|    `NORDLYNX_PRIVATE_KEY`     | NordVPN private key                                                                                   |         `my-nordlynx-private-key`         |
|  `MEDIA_SERVER_CONFIG_PATH`   | Path for config files                                                                                 |            `/path/to/configs`             |
|  `MEDIA_SERVER_MOVIES_PATH`   | Path for movies                                                                                       |             `/path/to/movies`             |
|    `MEDIA_SERVER_TV_PATH`     | Path for TV shows                                                                                     |               `/path/to/tv`               |
| `MEDIA_SERVER_DOWNLOADS_PATH` | Path for downloads                                                                                    |           `/path/to/downloads`            |
|      `STREMIO_HOSTNAME`       | Hostname for Stremio                                                                                  | `192-168-1-34.519b6502d940.stremio.rocks` |
|         `BAZARR_PORT`         | Port to access Bazarr                                                                                 |                  `6767`                   |
|        `JACKETT_PORT`         | Port to access Jackett                                                                                |                  `9117`                   |
|        `PROWLARR_PORT`        | Port to access Prowlarr                                                                               |                  `9696`                   |
|   `QBITTORRENT_WEBUI_PORT`    | Port to access qBittorrent Web UI                                                                     |                  `8090`                   |
|         `RADARR_PORT`         | Port to access Radarr                                                                                 |                  `7878`                   |
|         `SONARR_PORT`         | Port to access Sonarr                                                                                 |                  `8989`                   |
|     `STREMIO_SERVER_PORT`     | Port to access Stremio server                                                                         |                  `12470`                  |
|     `STREMIO_WEBUI_PORT`      | Port to access Stremio Web UI                                                                         |                  `8080`                   |
|       `WIREGUARD_PORT`        | Port for WireGuard connections                                                                        |                  `51820`                  |

## Accessing services
After starting, you can access the services at (using the values from [.env.example](./.env.example)):

|   Service   | Port  | URL                                                    |
|:-----------:|:-----:|:-------------------------------------------------------|
|    Plex     | 32400 | `http://192.168.1.34:32400/web`                        |
|   Sonarr    | 8989  | `http://192.168.1.34:8989`                             |
|   Radarr    | 7878  | `http://192.168.1.34:7878`                             |
|   Bazarr    | 6767  | `http://192.168.1.34:6767`                             |
| qBittorrent | 8090  | `http://192.168.1.34:8090`                             |
|   Jackett   | 9117  | `http://192.168.1.34:9117`                             |
|  Prowlarr   | 9696  | `http://192.168.1.34:9696`                             |
|   Stremio   | 8080  | `https://192-168-1-34.519b6502d940.stremio.rocks:8080` |
|  WireGuard  | 51820 | UDP port for VPN connections                           |

## Configuration guides
1. **Plex**: Complete the initial setup wizard and add your media libraries
2. **Sonarr / Radarr**: Configure indexers (Jackett / Prowlarr) and download client (qBittorrent)
3. **qBittorrent**: Set network interface to NordLynx and configure appropriate ports
4. **WireGuard**: Scan the QR codes in `/config/wireguard/peerX` to connect mobile devices
5. **Stremio**: Set streaming server port to `https://192-168-1-34.519b6502d940.stremio.rocks:12470/`

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
Check container logs:
```bash
docker compose logs <service-name>
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License
[MIT](./LICENSE)
