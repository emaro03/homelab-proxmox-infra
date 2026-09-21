# Proxmox Infrastructure Layer

> Part of [homelab-hub](https://github.com/YOUR_USERNAME/homelab-hub). The hypervisor layer that everything else in the lab runs on.

## Overview

The lab currently runs on a single Proxmox VE host (Dell Optiplex 3040 — i7-6700T, 4c/8t @2.80GHz, 12GB RAM, 1TB SSD, no dedicated GPU), mixing:

- **LXC containers** for services that benefit from lightweight, direct hardware access (e.g. Jellyfin with iGPU passthrough — see [`homelab-jellyfin-transcoding`](https://github.com/YOUR_USERNAME/homelab-jellyfin-transcoding)).
- **Docker Compose stacks** (running inside a dedicated LXC or VM) for everything else — easier to version, update and reproduce than native LXC installs.

## What's in this repo

| Path | Contents |
|---|---|
| `docs/container-layout.md` | What runs where, and why (LXC vs. Docker, resource allocation) |
| `docs/backup-strategy.md` | How containers/VMs are backed up |
| `config/vzdump.conf.example` | Sanitized backup job config |
| `scripts/` | Small maintenance scripts (snapshot cleanup, health checks) |

## Current known issues

- **Slow boot/startup times after restarts** — actively being investigated. Suspected causes under review: LXC device passthrough re-initialization order, storage (SSD) latency on cold boot, or systemd unit ordering for dependent services.

## Open decision: NAS consolidation vs. staying on Proxmox

Currently weighing two paths for the next hardware refresh:

| Option | Pros | Cons |
|---|---|---|
| **UGREEN DXP2800 GT (NAS)** — consolidate everything | Simpler ops, purpose-built storage, lower power | Less flexible for compute-heavy services, migration effort |
| **Lenovo ThinkCentre M920Q** — stay on Proxmox | Keeps current architecture/knowledge, more compute headroom, room for local AI experiments | Still need separate storage solution, more moving parts to maintain |

This repo's `docs/decision-log.md` will be updated once the decision is made, including the reasoning — the goal is to document the *process*, not just the outcome.

## License

MIT — see [LICENSE](LICENSE).
