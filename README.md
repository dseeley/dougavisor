# dougavisor

Ansible playbook to build a bare-metal KVM hypervisor on Ubuntu Server.  Consists of two playbooks: `isobuild.yml` and `hostconfig.yml`


## isobuild.yml
Creates a bootable ISO from the original [Live Ubuntu Server ISO](https://releases.ubuntu.com/) with custom [autoinstall](https://ubuntu.com/server/docs/install/autoinstall) & [cloud-init](https://cloudinit.readthedocs.io/en/latest/index.html) parameters (networking, users, etc) to allow a deterministic, hands-off, automatic installation.

### Invocation:
```shell
ansible-playbook -e targethost=dougavisor -e os_id=ubuntu2204 isobuild.yml
ansible-playbook -e targethost=dougavisortest -e os_id=ubuntu2004 isobuild.yml
```


## hostconfig.yml
Installs kvm/qemu/libvirt and useful tooling ([cockpit](https://cockpit-project.org/)) for managing the KVM hypervisor

## Requirements
An inventory file must exist that contains the hypervisor within the group you are configuring.  e.g.:

```
[dougavisor]
dougavisor ansible_host=192.168.1.3 ansible_user='root' ansible_ssh_private_key_file='~/.ssh/id_rsa'

[dougavisortest]
dougavisor ansible_host=192.168.1.32 ansible_user='root' ansible_ssh_private_key_file='~/.ssh/id_rsa'
```

### Invocation:
```shell
ansible-playbook -e targethost=dougavisor -e os_id=ubuntu2204 hostconfig.yml -i inventory
ansible-playbook -e targethost=dougavisortest -e os_id=ubuntu2004 hostconfig.yml -i inventory
```

