Role: pve_vm_tune_api_v1

Purpose:
- Post-clone Proxmox VM tuning via API:
  cores/sockets/cpu/numa, memory/balloon, agent, boot order, scsihw, onboot, tags/description, optional disk resize.

Required vars:
- vmid
- pve_node (inventory host id of the Proxmox node, e.g. "pve")
- host_vars/<pve_node>.yml must contain:
  pve_api_host, pve_api_user, pve_api_token_id, vault_pve_token_secret
  optional: pve_api_port (default 8006), pve_api_validate_certs (default false)

Recommended usage order:
1) clone role
2) pve_vm_tune_api_v1
3) cloud-init role
4) hardening role
