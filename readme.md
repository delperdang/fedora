# general
```
sudo dnf upgrade -y
sudo shutdown -r now
```

# nvidia
```
sudo dnf install kernel-devel kernel-headers gcc make dkms acpid libglvnd-glx libglvnd-opengl libglvnd-devel pkgconfig -y
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm -y
sudo dnf install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm -y
sudo dnf makecache -y
sudo dnf install akmod-nvidia xorg-x11-drv-nvidia-cuda -y
sudo shutdown -r now
```

# x11
```
sudo dnf install plasma-workspace-x11 kwin-x11 -y
sudo shutdown -r now
```
in the bottom left of the login screen select x11

# docker
```
sudo dnf remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine -y
sudo dnf install dnf-plugins-core -y
sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo -y
sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-compose -y
sudo systemctl enable docker
sudo groupadd docker
sudo usermod -aG docker $USER
sudo shutdown -r now
```
add the following line to /etc/fstab and restart
```
/dev/disk/by-id/wwn-0x50014ee26ad4bf44-part1 /mnt/Elements auto nosuid,nodev,nofail,x-gvfs-show 0 0
```
start all docker containers by startup script
```
cd /mnt/Elements/code/bedrock
./scripts/startup.sh
cd /mnt/Elements/code/jellyfin
./scripts/startup.sh
cd /mnt/Elements/code/lexcredendi
./scripts/startup.sh
```

# chrome
```
sudo dnf install fedora-workstation-repositories -y
sudo dnf config-manager --set-enabled google-chrome -y
sudo dnf install google-chrome-stable -y
```

# vscode
```
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" | sudo tee /etc/yum.repos.d/vscode.repo > /dev/null
sudo dnf check-update -y
sudo dnf install code -y
```

# steam
```
sudo dnf config-manager --enable fedora-cisco-openh264 -y
sudo dnf install steam -y
```
download the latest release of proton ge [here](https://github.com/GloriousEggroll/proton-ge-custom/releases)
```
mkdir ~/.steam/root/compatibilitytools.d
cd ~/Downloads
tar -xf GE-Proton*.tar.gz -C ~/.steam/root/compatibilitytools.d/
```
create a shaders directory
```
mkdir ~/shaders
```
add the following lines to ~/.bashrc
```
export __GL_THREADED_OPTIMIZATION=1
export __GL_SHADER_DISK_CACHE=1
export __GL_SHADER_DISK_CACHE_PATH=~/shaders
```
install winetricks and protontricks
```
sudo dnf install winetricks -y
sudo dnf install protontricks -y
```

# vlc
```
sudo dnf install vlc -y
```

# shotcut
```
mkdir ~/appimages
```
download the shotcut appimage [here](https://www.shotcut.org/download) and place it in the apppimages directory