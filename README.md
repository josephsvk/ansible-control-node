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