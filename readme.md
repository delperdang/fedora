# general
```
sudo dnf upgrade -y
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
