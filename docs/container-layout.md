# Container Layout

| ID (example) | Type | Service | Why this type |
|---|---|---|---|
| 101 | LXC (unprivileged) | Jellyfin | Needs direct `/dev/dri` access for QSV; LXC avoids full GPU passthrough complexity of a VM |
| 102 | LXC / Docker host | *arr stack (Sonarr, Radarr, Prowlarr, etc.) | Docker Compose for easy stack versioning and updates |
| 103 | LXC / Docker host | n8n | Isolated from media stack; automation shouldn't compete for resources with transcoding |
| 104 | LXC | Uptime Kuma | Lightweight, always-on, monitors the rest of the lab |
| — | Host-level | UniFi OS Server | Runs closer to the network layer — see [`homelab-unifi-network`](https://github.com/YOUR_USERNAME/homelab-unifi-network) |

> Replace the example CTIDs above with your real ones (or keep them generic like this for the public repo).

## Resource allocation philosophy

With only 12GB RAM and 4 cores on the current host, the priority order when something needs to be throttled is:
1. Jellyfin transcoding (protected — this is the main user-facing service)
2. *arr stack (can queue, not latency-sensitive)
3. n8n (batch workflows, not latency-sensitive)
4. Uptime Kuma (minimal footprint by design)

This constraint is the main driver behind the hardware refresh decision — see the main README.
