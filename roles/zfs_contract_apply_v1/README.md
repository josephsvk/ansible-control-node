# roles/zfs_contract_apply_v1/README.md

# zfs_contract_apply_v1
Applies enterprise storage contract to ZFS:
- creates missing datasets (non-destructive)
- sets/overrides ZFS properties per policy (idempotent)
- does NOT delete existing datasets by default (legacy stays)
- supports future delete mode (disabled now)

Run on Proxmox host that owns the ZFS pools (pve).