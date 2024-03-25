# Ansible
My ansible scripts 

## Running playbook ( Patching ) 
This Playbook will update all the yum and apt hosts 

```bash
 ansible-playbook update_playbook.yaml
#I have moved over to using Ansible-vault to store the sudo password so this changes the command used to run the update_playbook script
ansible-playbook  -vv --ask-vault-pass --extra-vars '@passwd.yaml' update_playbook.yaml
# you will be prompted to enter the password for the Vault 
```


## Ansible-Vault 

we need to create the secret in Ansible-vault, to do this lets create a yaml file with our sudo passowrd 

```bash
echo "ubuntu_sudo_user: Pa55W0RD123" > passwd.yaml
ansible-valut encrypt passwd.yaml

you will be promted twice to set a password 

you can use decrypt if you ever needed to decode the password
```


This play book is to reboot MotionEye servers ( bit of a unique one as the /root is all Read Only so have to redirect to a mountpoint thats ansible can write to ) 
```bash
 ansible-playbook reboot_CCTV.yaml
```

## Installing Ansible on Rocky Linux ( only need to do this on the Ansible server) 

```bash
yum install epel-release
yum install ansible
```

## Create the Ansible SSH key ( only need to do this once) 

```bash
ssh-keygen -C "ansible"
```
## Copy the key to the servers ( need to do this for each server) 

This command copys the ssh key to the desired host note you may need to spefify the username if not running as root, you may also be prompted for the password of the server

```bash
ssh-copy-id -i /root/.ssh/ansible docker.local
```
once copied check that you can ssh to the server using the key e.g.

```bash
ssh -i /root/.ssh/ansible docker.local
```

## sanity check ansible can reach the clients 
This is a usefull part of ansible make sure that ansible can ping the servers. 

```bash
ansible all -m ping --key-file ~/.ssh/ansible
```

```yaml
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
```
