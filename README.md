sudo nano /etc/resolv.conf

test configu : 
ansible --version
ansible-config dump --only-changed

test inventory : 
ansible-inventory --graph
ansible -m ping all --ask-pass

###############
ansible-playbook playbooks/bootstrap.yml --ask-pass --become --ask-become-pass

zmena usera v hosts > ansible
# Bootstrap :
    - timezone
    - update
    - add ssh key 
    - add user ansible 
    - add grup 
    - add sudo to ansible 


# wokrstation instalacia 

    - zmena usera na joseph potom na ansible 
    - najprv použit spustienie z heslom aj pre sudo ked treba 
        --ask-pass --become --ask-become-pass
    -

### edit valut !!! 

priprava kluču 

mkdir -p ~/.config/ansible
chmod 700 ~/.config/ansible
openssl rand -base64 48 > ~/.config/ansible/vault-pass-prod
chmod 600 ~/.config/ansible/vault-pass-prod

vytvorenie vault 

ansible-vault create \
  inventories/lab/group_vars/all/vault.yml \
  --vault-password-file ~/.config/ansible/vault-pass-prod

export EDITOR="code --wait"

ansible-vault edit inventories/lab/group_vars/all/vault.yml \
  --vault-password-file ~/.config/ansible/vault-pass-prod

# krok po kroku vyvoj a testovanie upravy konfigu step 1 pridanie testovanych zniem 

    povoleni prihlasenia sa pomocou ssh key 
    bude potrebn pridat ešte spravny key 
    


root > inštalacia sudo a usera ansible 
ansible user > inštalacia klučov ssh 

# testovanie 
 
 ansible-playbook -i inventories/lab/hosts.yml playbooks/bootstrap_root_v1.yml --ask-pass --limit pve1


