# Ansible
My ansible scripts 

## Running playbook ( Patching ) 
This Playbook will update all the yum and apt hosts 

```bash
 ansible-playbook update_playbook.yaml
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
