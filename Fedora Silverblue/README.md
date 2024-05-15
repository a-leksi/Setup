# Fedora Silverblue Setup

## Install

Create the installation media with [Fedora Media Writer](https://fedoraproject.org/fr/workstation/download)

## Setup

### Reboot 
> You will need to reboot multiple time basically in each step.

Reboot command:
```bash
systemctl reboot
```

### Update
Update, upgrade and reboot:
```bash
rpm-ostree update && rpm-ostree upgrade
```

### Rebase - Universal Blue
Community Fedora Silverblue images - optionally with NVIDIA drivers built-in.

#### Ublue Main
Rebase command:
```bash
rpm-ostree rebase ostree-unverified-registry:ghcr.io/ublue-os/silverblue-main:latest
```

#### Ublue NVIDIA
Rebase command:
```bash
rpm-ostree rebase ostree-unverified-registry:ghcr.io/ublue-os/silverblue-nvidia:latest
```
After reboot configure nvidia using ujust
```bash
ujust configure-nvidia
```
### Packages

Add [VSCode](https://code.visualstudio.com/docs/setup/linux#_rhel-fedora-and-centos-based-distributions) repo:
```bash
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
```

Install VSCode, Podman, Python:
```bash
rpm-ostree install code podman-docker python3-pip python3-virtualenv gnome-shell-extension-dash-to-dock
```

### Config

Setup Vscode:
> DockerExtension 1.22.2

Enable the podman socket
```bash
systemctl enable --now --user podman.socket
```

Add this config to settings.json
```txt
"docker.host": "unix:///run/user/1000/podman/podman.sock",
"docker.dockerPath": "/usr/bin/podman"
```

Disable pip outside virtualenv
```bash
pip config set global.require-virtualenv True
```





