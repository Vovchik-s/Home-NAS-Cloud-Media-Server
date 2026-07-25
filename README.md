# 🏠 Synology NAS – Self-Hosted Homelab & Private Cloud

This repository documents the architecture and service deployment for a **Synology NAS** transformed into a full-fledged **Self-Hosted Homelab**. Powered by Docker, this setup serves as a private family cloud, automated media server, knowledge platform, and secure automation engine — built with Zero Trust security and high availability in mind.

---

## 🚀 Project Overview

- **Private Family Cloud**: Secure photo/document storage with snapshot-based ransomware protection.
- **Automated Media Ecosystem**: Fully integrated *Arr stack with VPN-isolated torrent client and direct Jellyfin streaming.
- **Productivity & Knowledge Hub**: Centralized documentation, task management, recipe planning, and digital library.
- **Automations & Microservices**: Self-hosted n8n workflows, financial alerts, and custom API backends.
- **Zero Trust Ingress**: Remote access powered by Cloudflare Tunnels without opening router ports.

---

## 🛠️ Tech Stack & Deployed Services

| Category | Service | Description |
| :--- | :--- | :--- |
| **Media & Streaming** | **Jellyfin** | Open-source media server for streaming movies and TV shows |
| | **Jellyseerr** | User-friendly media discovery and request management UI |
| | **Radarr / Sonarr** | Automated movie and TV series collection management |
| | **Prowlarr / Bazarr** | Indexer management and automated subtitle downloads |
| | **qBittorrent + Gluetun** | Download client force-routed through a PIA VPN gateway for anonymity |
| **Productivity & Docs** | **Docmost** | Real-time collaborative wiki and knowledge management platform |
| | **Vikunja** | Task management and project planning platform |
| | **Mealie** | Self-hosted recipe manager and meal planner |
| | **Calibre-Web** | Web interface for browsing and downloading e-books |
| | **Omni-Tools** | Self-hosted collection of web-based developer and IT utilities |
| **Automation & Custom** | **n8n** | Workflow automation engine connecting internal and external APIs |
| | **STRUKT Platform** | Custom API microservice platform backed by PostgreSQL |
| | **Finance Alerts** | Automated financial alert monitoring system |
| **Infrastructure & Ops** | **Cloudflare Tunnel** | Encrypted, port-forward-free ingress remote access |
| | **Portainer** | Container management UI for Docker stacks and volumes |
| | **Grafana** | Infrastructure analytics and performance metrics monitoring |
| | **Synology DSM** | Core host OS (Btrfs snapshots, RAID, storage pools, SSD caching) |

---

## 🛡️ Security & Infrastructure Architecture

[ External User ] ──( Cloudflare Tunnel )──> [ Synology NAS (Docker) ]
│
┌───────────────────┼───────────────────┐
▼                   ▼                   ▼
[ Apps & UI ]     [ *Arr Pipeline ]   [ Storage (Btrfs) ]
(Docmost, Jellyfin)        │             (Snapshots & RAID)
▼
[ Gluetun VPN ]
│
▼
[ qBittorrent ]


- **Zero Open Ports**: Router ports remain strictly closed. Remote ingress is secured via `cloudflared` tunnels.
- **Network Isolation**: Downloading via `qBittorrent` is strictly bound to the `Gluetun` VPN container network namespace (`network_mode: "service:gluetun"`).
- **Atomic Operations & Hardlinks**: Shared Docker volumes mapped across media containers to allow instant hardlinking without duplicating disk usage.
- **Data Protection**: Automated snapshot replication, Btrfs integrity checks, and scheduled off-site backups.

---

## 📦 Future Improvements

- [ ] Complete custom Grafana dashboards for Docker resource monitoring and VPN bandwidth tracking.
- [ ] Implement automated container updates via Watchtower / Renovate.
- [ ] Set up immutable off-site backups (S3 / Hyper Backup).

---

## 📁 License

This repository contains configuration notes, compose files, and architecture documentation for educational and home lab reference.

---

## 🙋‍♂️ Maintainer

**Vladimir Mizkevich**  
[LinkedIn](https://www.linkedin.com/in/vladimir-mizkevich) • [GitHub](https://github.com/yourusername)
