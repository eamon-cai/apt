# Debian8 
```
DEBIAN_FRONTEND=noninteractive apt-get install -y curl screen nload p7zip-full nginx vnstat gawk spawn-fcgi libfcgi0ldbl fcgiwrap unzip mysql-server mysql-client php php-mysql php-cgi php-gd php-sqlite3 php-curl python3-pip ipset cadaver iftop
```

# Debian8/9 Kernel
```
bash <(wget --no-check-certificate -qO- 'https://moeclub.org/attachment/LinuxShell/Debian_Kernel.sh')
```

# Debian8/9 LotServer
```
bash <(wget --no-check-certificate -qO- https://github.com/MoeClub/lotServer/raw/master/Install.sh) uninstall
```

# Debian8/9 Nginx
```
wget --no-check-certificate -qO- 'https://moeclub.org/attachment/LinuxShell/nginx_update.sh' |bash
```

# Linux limits
```
[ -f /etc/security/limits.conf ] && LIMIT='262144' && sed -i '/^\(\*\|root\)[[:space:]]*\(hard\|soft\)[[:space:]]*\(nofile\|memlock\)/d' /etc/security/limits.conf && echo -ne "*\thard\tmemlock\t${LIMIT}\n*\tsoft\tmemlock\t${LIMIT}\nroot\thard\tmemlock\t${LIMIT}\nroot\tsoft\tmemlock\t${LIMIT}\n*\thard\tnofile\t${LIMIT}\n*\tsoft\tnofile\t${LIMIT}\nroot\thard\tnofile\t${LIMIT}\nroot\tsoft\tnofile\t${LIMIT}\n\n" >>/etc/security/limits.conf

```

# ReInstall
```
bash <(wget --no-check-certificate -qO- 'https://raw.githubusercontent.com/MoeClub/Note/master/InstallNET.sh') -d 9 -v 64 -a
```

# Install Win8.1
```
bash <(wget --no-check-certificate -qO- 'https://raw.githubusercontent.com/MoeClub/Note/master/InstallNET.sh') -dd "https://api.moeclub.org/redirect/win8.1emb_x64.tar.gz"
```

# Timezone
```
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
echo "Asia/Shanghai" >/etc/timezone
```

# Root
```
#!/bin/bash
echo root:Vicer |sudo chpasswd root
sudo sed -i 's/^#\?Port.*/Port 22/g' /etc/ssh/sshd_config;
sudo sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin yes/g' /etc/ssh/sshd_config;
sudo sed -i 's/^#\?PasswordAuthentication.*/PasswordAuthentication yes/g' /etc/ssh/sshd_config;
sudo reboot
```

# Windows Image
```
# win7emb_x86.tar.gz:
https://api.moeclub.org/GoogleDrive/1srhylymTjYS-Ky8uLw4R6LCWfAo1F3s7 
https://api.moeclub.org/redirect/win7emb_x86.tar.gz

# win8.1emb_x64.tar.gz:
https://api.moeclub.org/GoogleDrive/1cqVl2wSGx92UTdhOxU9pW3wJgmvZMT_J
https://api.moeclub.org/redirect/win8.1emb_x64.tar.gz

# win10ltsc_x64.tar.gz:
https://api.moeclub.org/GoogleDrive/1OVA3t-ZI2arkM4E4gKvofcBN9aoVdneh
https://api.moeclub.org/redirect/win10ltsc_x64.tar.gz
```

# Linux sysctl.conf
```
# This line below add by user.
fs.file-max = 104857600
fs.nr_open = 1048576
vm.overcommit_memory = 1
net.ipv4.ip_forward = 1
net.core.somaxconn = 4096
net.core.optmem_max = 262144
net.core.rmem_max = 8388608
net.core.wmem_max = 8388608
net.core.rmem_default = 262144
net.core.wmem_default = 262144
net.core.netdev_max_backlog = 65536
net.ipv4.tcp_mem = 262144 6291456 8388608
net.ipv4.tcp_rmem = 16384 262144 8388608
net.ipv4.tcp_wmem = 8192 262144 8388608
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_syn_retries = 4
net.ipv4.tcp_synack_retries = 3
net.ipv4.tcp_max_syn_backlog = 4096
net.ipv4.tcp_fin_timeout = 24
net.ipv4.tcp_keepalive_intvl = 32
net.ipv4.tcp_keepalive_probes = 3
net.ipv4.tcp_keepalive_time = 900
net.ipv4.tcp_retries1 = 3
net.ipv4.tcp_retries2 = 8
#net.ipv4.icmp_echo_ignore_all = 1
net.ipv4.tcp_timestamps = 1
net.ipv4.tcp_slow_start_after_idle = 0
#net.ipv4.tcp_fastopen = 3
#net.core.default_qdisc = fq
#net.ipv4.tcp_congestion_control = bbr

```

# Run with user
```
start-stop-daemon --start --quiet --chuid "<USER>" --name "<ExecName>" --exec "<ExecPath>" -- <ARGVS>

```

# scp
```
scp -P 22 -r <DIR> user@host:<DIR>

```

# rcone
```
./rclone copy --no-check-certificate --progress --checksum --min-size 50M --multi-thread-streams 8 --transfers 8 --drive-shared-with-me

```

# nvm, nodejs, npm
```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash

# nvm ls-remote | grep LTS
nvm install v8.9.0
npm install --global gulp-cli

```

# nload
```
echo -ne 'DataFormat="Human Readable (Byte)"\nTrafficFormat="Human Readable (Byte)"\n' >/etc/nload.conf

```

# ntpdate
```
ntpdate -4 time.windows.com time.apple.com

```

# fstab
```
fdisk /dev/sdc #[g,n,w]
mkfs -t ext4 /dev/sdc1

mkdir -p /data
dev=/dev/sdc1
if [ -f /etc/fstab ]; then
  sed -i "/$(basename ${dev})/d" /etc/fstab
  while [ -z "$(sed -n '$p' /etc/fstab)" ]; do sed -i '$d' /etc/fstab; done
  sed -i "\$a${dev}\t/data\text4\tdefaults,nofail,noatime,nodiratime,nobarrier\t0\t2\n\n" /etc/fstab
fi

# /dev/sdc /data ext4 defaults,nofail,noatime,nodiratime,nobarrier 0 2

```

# journalctl
```
# disable
sed -i 's/^#\?Storage=.*/Storage=none/' /etc/systemd/journald.conf

# keep & limit in memory
sed -i 's/^#\?Storage=.*/Storage=volatile/' /etc/systemd/journald.conf
sed -i 's/^#\?SystemMaxUse=.*/SystemMaxUse=8M/' /etc/systemd/journald.conf
sed -i 's/^#\?RuntimeMaxUse=.*/RuntimeMaxUse=8M/' /etc/systemd/journald.conf

# restart service
systemctl restart systemd-journald
systemctl status systemd-journald

# watch 
journalctl -f -u <service.name>

# manual
journalctl --rotate

journalctl --vacuum-size=8M
journalctl --vacuum-files=1
journalctl --vacuum-time=7d
```

# nvidia & cuda
```
echo "deb http://deb.debian.org/debian/ buster main contrib non-free" >>/etc/apt/sources.list
apt update
DEBIAN_FRONTEND=noninteractive apt install -y nvidia-driver nvidia-cuda-toolkit nvidia-kernel-dkms firmware-misc-nonfree

# nvidia-smi
# apt install -y "linux-headers-`uname -r`"
# sudo dkms install -m `ls -1 /usr/src |grep "^nvidia" |sed 's/^nvidia-/nvidia\//'`
```
