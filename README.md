# Ansible Podman Wirehole

## Requirements

For now, only works with remote servers using Oracle Linux 8

## Dependencies

### Install ansible

I prefer installing ansible with pip, but you can try [other options](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

#### Install pip

```sh
sudo apt install python3-pip
```

#### Install ansible with pip

```sh
python -m pip install --user ansible
```

### Install ansible collections

```sh
ansible-galaxy collection install community.general
ansible-galaxy collection install containers.podman
ansible-galaxy collection install ansible.posix
```

## Setup

### Run your ssh agent

First of all, make sure your ssh key is added in a running ssh-agent.
Otherwise, you might be prompted to type your passphrase more than often.

```sh
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

### Host file method

#### Create a host file

Create a file named `host` and don't forget to replace `SERVER-IP` and `USERNAME`.

```ini
[remotehost]
SERVER-IP

[remotehost:vars]
ansible_ssh_user=USERNAME
ansible_ssh_private_key_file=~/.ssh/id_rsa
```

#### Run ansible-playbook

```sh
ansible-playbook -i host main.yml
```

### Passing arguments method

```sh
ansible-playbook -i SERVER-IP, -u USERNAME main.yml
```

**Comma is not a typo!**

## Using

You can use any of the peer configs in `peers` folder created in the same directory as where you run ansible-playground.

To connect to your vpn server:

- Import `peerN.conf` for WireGuard desktop client.
- Scan `peerN.png` for the mobile app.

When connected to vpn, pihole web interface is accesible through [http://10.2.0.100/](http://10.2.0.100/)

Login password for pihole web interface is saved in `credentials/pihole` file.

## See also

- [wirehole](https://github.com/IAmStoxe/wirehole)
- [terransible-wirehole](https://github.com/mjtechguy/terransible-wirehole)
