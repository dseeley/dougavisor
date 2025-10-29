# dougavisor

Ansible playbook to build a bare-metal KVM hypervisor on Ubuntu Server.

Installs kvm/qemu/libvirt and useful tooling ([cockpit](https://cockpit-project.org/)) for managing the KVM hypervisor

## isobuild.yml
Creates a bootable ISO from the original [Live Ubuntu Server ISO](https://releases.ubuntu.com/) with custom [autoinstall](https://ubuntu.com/server/docs/install/autoinstall) & [cloud-init](https://cloudinit.readthedocs.io/en/latest/index.html) parameters (networking, users, etc) to allow a deterministic, hands-off, automatic installation.

### Invocation:
```shell
ansible-playbook -e targethost=dougavisor -e os_id=ubuntu2404 isobuild.yml
ansible-playbook -e targethost=dougavisortest -e os_id=ubuntu2404 isobuild.yml
```

## Burn image to USB
Use Rufus with default settings to burn the image to a USB stick.
