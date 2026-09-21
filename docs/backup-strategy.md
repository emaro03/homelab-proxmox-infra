# Backup Strategy

_Fill this in with your actual approach. Suggested structure below._

## What's backed up

- [ ] Proxmox `vzdump` snapshots of all LXCs/VMs — schedule and retention
- [ ] Docker Compose stacks — are `docker-compose.yml` + bind-mount data backed up separately from vzdump?
- [ ] Config files kept in this repo (sanitized) vs. real configs kept elsewhere (password manager / private repo)

## Where backups go

- [ ] Local (second disk?) / offsite / cloud — document the 3-2-1 posture honestly, even if it's incomplete today. Recruiters reading this respect "here's what I have and here's the gap I know about" more than a fake-complete picture.

## Restore testing

- [ ] Last time a restore was actually tested end-to-end (if never — that's worth noting as a known gap and a next step).
