# proxmox_access_mgmt

Idempotent správa Proxmox VE: pools, roles, users, tokens (privsep), ACL.

## Requirements
- bežať na Proxmox node (alebo delegate_to na node) s root
- príkazy: pveum, pvesh

## Usage
Nastav `proxmox_access` v group_vars/host_vars a pridaj rolu do playbooku.