# Ansible
My ansible scripts 


Running the update 

 ansible-playbook update_playbook.yaml

Installing Ansible on Rocky Linux 
yum install epel-release
yum install ansible

Create the Ansible SSH key 
ssh-keygen -C "ansible"

Copy the key to the servers 
ssh-copy-id -i /root/.ssh/ansible docker.local

sanity chcek ansible can reach the clients 
ansible all -m ping --key-file ~/.ssh/ansible

vpn.local | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
docker.local | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
192.168.1.233 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
navidrome.local | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
