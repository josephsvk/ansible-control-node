**dočasny ssh kluč**

```console
mkdir -p ~/.ssh
chmod 700 ~/.ssh

ssh-keygen -t ed25519 -a 64 -f ~/.ssh/hetzner_bootstrap_ed25519 -C "hetzner-bootstrap-$(hostname)-$(date +%F)" -N ""
chmod 600 ~/.ssh/hetzner_bootstrap_ed25519
chmod 644 ~/.ssh/hetzner_bootstrap_ed25519.pub

cat ~/.ssh/hetzner_bootstrap_ed25519.pub
```

**Pridaj verejný kľúč do Hetzner**

ansible-playbook -i inventories/prod/hosts.yml playbooks/bootstrap_root_v1.yml --limit 'bootstrap:&vps-hetz-1'

**ak je proble postupuj takto**

```console
mkdir -p /root/.ssh
chmod 700 /root/.ssh
cat >> /root/.ssh/authorized_keys <<'EOF'
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIA7cJybBMCUcVziAfH1BvFTbq6UozMOvpEfRs1vSEz3O hetzner-bootstrap-Ansible-Control-Node-2026-02-01
EOF
chmod 600 /root/.ssh/authorized_keys
```

teraz si pridal pup do servera 

overenie či sa spravne prešiel bootsrap 

ansible -i inventories/lab/hosts.yml vps-hetz-1 -m ping --limit managed -vv

ansible -i inventories/lab/hosts.yml vps-hetz-1 -m command -a 'id' --become --limit managed

ansible-inventory -i inventories/lab/hosts.yml --host vps-hetz-1 | egrep 'ansible_user|ansible_ssh_private_key_file|ansible_become'

ansible -i inventories/lab/hosts.yml vps-hetz-1 -m shell -a 'sudo -n true && echo SUDO_OK || echo SUDO_FAIL; ls -la ~/.ssh; sudo ls -la /home/ansible/.ssh; sudo cat /home/ansible/.ssh/authorized_keys' --limit managed

