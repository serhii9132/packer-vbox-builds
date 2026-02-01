# packer-vbox-builds

Automated VirtualBox image builds defined in YAML. Uses [packer-config-gen](https://github.com/serhii9132/packer-config-gen) to dynamically generate Packer manifests and boot command files from a single source of truth.

### Supported Packer builder:
- [virtualbox-iso](https://developer.hashicorp.com/packer/integrations/hashicorp/virtualbox/latest/components/builder/iso)

### Available OS Images:
- Debian 13.3
- Ubuntu 24.04.3 LTS

### Template details:
- CPU: 2 cores
- Disk: 150 Gb
- RAM: 4 Gb
- Partitioning: LVM
- Swap: disabled
- USB: disabled
- Audio: disabled
- Firmware: EFI
- Preinstalled packages: python3, wget, rsync, bash-completion
- User: with sudo privileges is created without password prompt or root

### Prerequisites:
- [Vagrant](https://developer.hashicorp.com/vagrant)
- [Packer](https://developer.hashicorp.com/packer)
- [VirtualBox and VirtualBox Extension Pack](https://www.virtualbox.org/wiki/Downloads)
- [Python 3.13](https://www.python.org/)
- [packer-config-gen](https://pypi.org/project/packer-config-gen/)

## Usage
### 1.Environment setup
Create a .env file in the root of the project with the following content:
```sh
export USERNAME="user"
# Use: mkpasswd -m sha-512
export PASSWORD='$6$vPP.....'

export SSH_PUBLIC_KEY='ssh-ed25519 AAAAbbbbbbbccccccc....'
export SSH_PRIVATE_KEY_FILE="/home/user/.ssh/key"
```

### 2.Configuration generation
To generate build artifacts (HCL and HTTP files), use:
```sh
make ubuntu
make debian
```
After execution, the generated files will appear in the artifacts/{ubuntu|debian}/ directory and the OS build process will start. Vagrant images will be available at artifacts/${OS_NAME}/builds

### Tested with:
- Packer: v1.14.3
- packer-plugin-vagrant: 1.1.6
- packer-plugin-virtualbox: 1.1.3
- VirtualBox: 7.2.4
- Vagrant: 2.4.9