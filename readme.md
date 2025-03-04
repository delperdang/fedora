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
sudo dnf install plasma-workspace-x11 kwin-x11 -y
sudo shutdown -r now
```

# docker
```
sudo dnf install moby-engine docker-cli containerd docker-buildx docker-compose docker-compose-switch -y
sudo systemctl enable docker
sudo groupadd docker
sudo usermod -aG docker $USER
```
add the external drive to fstab as "d"
```
echo "/dev/disk/by-id/wwn-0x50014ee26ad4bf44-part1 /mnt/d auto nosuid,nodev,nofail,x-gvfs-show 0 0" | sudo tee -a /etc/fstab
sudo shutdown -r now
```
start the docker container by startup script
```
cd /mnt/d/code/jellyfin
./scripts/startup.sh
```

# chrome
```
sudo dnf install fedora-workstation-repositories -y
sudo dnf config-manager setopt google-chrome.enabled=1
sudo dnf install google-chrome-stable -y
```

# vscode
```
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\nautorefresh=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" | sudo tee /etc/yum.repos.d/vscode.repo > /dev/null
sudo dnf check-update -y
sudo dnf install code -y
```

# vlc
```
sudo dnf upgrade -y
sudo dnf group upgrade multimedia -y
sudo dnf install libavcodec-freeworld --allowerasing -y
sudo dnf install vlc -y
sudo shutdown -r now
```

# steam
```
sudo dnf install steam -y
```
run steam once and activate compatibility then download the latest release of [proton ge](https://github.com/GloriousEggroll/proton-ge-custom/releases) to ~/Downloads
```
cd ~/Downloads
tar -xf GE-Proton*.tar.gz -C ~/.steam/root/compatibilitytools.d/
rm GE-Proton*.tar.gz
mkdir ~/shaders
echo "export __GL_THREADED_OPTIMIZATION=1" | sudo tee -a ~/.bashrc
echo "export __GL_SHADER_DISK_CACHE=1" | sudo tee -a ~/.bashrc
echo "export __GL_SHADER_DISK_CACHE_PATH=~/shaders" | sudo tee -a ~/.bashrc
sudo dnf install winetricks -y
sudo dnf install protontricks -y
```

# input remapper
```
sudo dnf install input-remapper -y
sudo systemctl enable --now input-remapper
```

# sunshine
```
sudo dnf copr enable lizardbyte/stable -y
sudo dnf install sunshine -y
systemctl --user enable sunshine
systemctl --user start sunshine
sudo loginctl enable-linger $USER
systemctl --user daemon-reexec
```