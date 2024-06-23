# Media-Server-Project

Emby

Media Server Setup Documentation..
File Structuring..
The file structure is organized as follows: the main Media directory contains a Downloads subfolder, which is further divided into TV Shows and Movies subfolders. Sonarr is configured to connect to the TV Shows subfolder, Radarr to the Movies subfolder, and qBitTorrent to the Downloads subfolder.

Requests: Ombi
To set up Ombi, begin by downloading the ZIP file from GitHub. Create a desktop shortcut of the .exe file and place it in the Startup Programs folder to ensure Ombi starts with Windows. Configure Ombi to run on Port 5000 of your localhost. Start the Ombi server and access the backend by entering localhost:5000 in your web browser. Set up an Admin account and disable authentication if operating on a local network. Connect Ombi to Prowlarr, Radarr, Sonarr, and Emby using API keys and your IPv4 address. Ensure each web media server in Ombi checks for availability, then test each connection and troubleshoot any logged issues. If necessary, disable authentication within your local network.

Top Layer: Emby
Emby serves as the primary media server for playing media. Connect Ombi, Prowlarr, Radarr, and Sonarr to Emby using API keys and IPv4 addresses. Configure Emby to access the file structure in order to retrieve downloaded media.

Middle Layers
Sonarr and Radarr operate as the middle layers. Sonarr manages TV show downloads, placing them into the TV Shows folder. It connects to Ombi, Prowlarr, Radarr, and Emby, and operates on Port 8989. Radarr manages movie downloads, placing them into the Movies folder. It connects to Ombi, Prowlarr, Sonarr, and Emby, and operates on Port 7878.

Bottom Layers
qBitTorrent and Prowlarr form the bottom layers. qBitTorrent is the torrent client, connected to Emby, Ombi, Radarr, Sonarr, and Prowlarr. It operates on Port 8080 and is configured with a Socks5 Proxy using Mullvad VPN (IP Address 10.8.0.1 and Port 1080). qBitTorrent downloads to the Downloads subfolder, associates files with .torrent and magnet links, switches the peer connection protocol to TCP, and disables UPnP/NAT-PMP port forwarding. Authentication is disabled unless enhanced security is desired. BitTorrent options include disabling all privacy options except encryption and anonymous mode, and setting the network interface to Mullvad VPN. The Web UI is enabled, with the IP address set to a wildcard *, localhost, or the IPv4 address, and authentication bypassed for clients on localhost.

Prowlarr acts as the indexer, searching for torrents and magnet links based on Ombi requests. It operates on Port 9696. Prowlarr connects to both public and private indexers, handling Cloudflare's authentication using FlareSolverr, configured at http://flaresolverr:8191/. Prowlarr connects to Ombi, Emby, Radarr, and Sonarr via API keys and IPv4 address.

VPN: Mullvad
Mullvad VPN provides privacy and a Socks5 proxy. It is configured to run on OpenVPN, although WireGuard can also be used.

Proxy: Socks5
The Socks5 Proxy is integrated with Firefox, Mullvad, and qBitTorrent. In Firefox, navigate to network settings, enable manual proxy configuration, leave the HTTP and HTTPS proxy fields empty, and set the SOCKS Host to IP 10.8.0.1 and Port 1080.

Workflow Summary
The structured setup operates as follows: Users request TV shows or movies via Ombi. The admin approves the requests, which are then processed by Prowlarr. Prowlarr searches for the media and sends it to qBitTorrent for downloading. qBitTorrent sorts and places the media into the correct folders. The media is then accessed and played through Emby. This setup ensures a seamless and organized media server experience.

File structuring
Media
->Downloads
-->TV Shows
-->Movies
