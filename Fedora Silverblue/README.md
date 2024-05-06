# Fedora Silverblue Setup

Create the installation media with [Fedora Media Writer]()

## Post-install

### Update
Update, upgrade and reboot:
```bash
rpm-ostree update && rpm-ostree upgrade && systemctl reboot
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
rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/silverblue-nvidia:latest
```

### Dash-to-dock
Install dash-to-dock extension:
```bash
rpm-ostree install \
gnome-shell-extension-dash-to-dock \
```

#### VSCode
Add [VSCode](https://code.visualstudio.com/docs/setup/linux#_rhel-fedora-and-centos-based-distributions) repo:

```bash
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
```

Install VSCode:

```bash
rpm-ostree install code
```
