

# Linux

Including all the notes related with installation of linux systems and the setups in linux.

Test io speed:

```shell
dd if=/dev/zero of=test.file bs=64M count=32 oflag=dsync
```





## Linux Sever

**Configure the apt source for Debian/Ubuntu**

Change the nickname of the system version `buster` to yours

```txt
deb http://ftp.debian.org/debian buster main contrib non-free
deb http://ftp.debian.org/debian buster-updates main contrib non-free
deb http://security.debian.org buster/updates main contrib non-free
deb http://ftp.debian.org/debian buster-backports main contrib non-free
```



**SSH**

Change the configuration file in `/etc/sshd.config`, change the port to your desired port

```shell
echo "Port 2000" >> /etc/sshd.conf
systemctl restart sshd.service
systemctl status sshd.service
```

**add user**

```shell
# Adding new user in Linux:
adduser --shell /bin/zsh hang
useradd -m -d /var/www/ravi -s /bin/bash -c "TecMint Owner" -U ravi
useradd -G admins,webadmin,developers tecmint

```

**Security**

generate authentication:

apache2-utils:

Basic: htpasswd -c /etc/nginx/.htpasswd username

Digest: htdigest -c /etc/apache2/users.password webdav username

add new user: htdigest /etc/apache2/users.password webdav new_user

ref: [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-configure-webdav-access-with-apache-on-ubuntu-14-04)

 

### SSL

各种不同的证书参见 [link](https://www.cnblogs.com/guogangj/p/4118605.html)

openssl req -newkey rsa:2048 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem

 generate authentication:

```shell
# apache2-utils
#>> Basic
htpasswd -c /etc/nginx/.htpasswd username
#>> Digest
htdigest -c /etc/apache2/users.password webdav username

#adding new user: 
htdigest /etc/apache2/users.password webdav new_user
```

```shell
# generate ssh key and upload to the server
ssh-keygen
ssh-copy-id name@linuxserver
```





## Linux on VirtualBox

For Debian based distributions, the easiest way to install the guest 

```shell
sudo apt install virtualbox-guest-x11 virtualbox-guest-utils virtualbox-guest-dkms
```

Most recently [instructions](https://www.linuxuprising.com/2019/01/manual-virtualbox-guest-additions.html). In short, to install the VirtualBox guest features from the external iso, you need to install the requisites:

```shell
sudo apt install gcc make perl dkms
```

To run the install script:

```shell
sudo sh /media/cdrom0/VBoxLinuxAdditions.run
```

The most secure method is by inserting the VirtualBox guest iso



To use the share folder, put yourself in the vboxsf group 

```shell
sudo usermod -aG vboxsf $USER
```



## Raspberry Pi

### Locale

Set the local: editing the '/etc/default/locale'

```shell
LC_ALL=C
LANG=en_US.UTF-8
LANGUAGE=en_US.UTF-8
```

### WiFi

```
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```

At the bottom of this file, add the following lines.

```
network={
ssid="wifi name"
psk="wifi Password"
}
```





## Termux

install numpy and scipy: https://github.com/its-pointless

install astropy: 

```shell
CC=clang
apk install clang
pip install astropy #the samw for pandas
```



## Reset the lost root passwd

At the start of normal startup, press `e` to edit the startup items.

The move the Linux16 line, then change the:

```shell
rhgb quiet ==> rd.break enforcing=0
```

to make the system login into the emergency mode, then change root by:

```
# mount –o remount,rw /sysroot
# chroot /sysroot
```

Then you can rest the root password by `passwd`

After that:

```
# restorecon -v /etc/shadow
# setenforce 1
```

to make the system back to the SELinux enforcing mode.

Reference: https://opensource.com/article/18/4/reset-lost-root-password 



## Chroot

Before mount the root system from the live-cd, it is wisable to check their size and properties, so that you can guess its usage.

```shell
# to print all the disks avaible
blkid

# to check whether boot and efi are stand alone
grep boot /etc/fstab
```



```shell
 mkdir /mnt/sysimage
 
 mount /dev/mapper/fedora-root /mnt/sysimage
 # mount /boot and /efi if their are on seperated patition
 mount /dev/sda8 /mnt/sysimage/boot
  
 for dir in /dev /proc /sys; do mount --bind $dir /mnt/sysimage/$dir ; done
 chroot /mnt/sysimage
```



https://docs.fedoraproject.org/en-US/Fedora/22/html/Multiboot_Guide/common_operations_appendix.html



## Raid

[Raid setup](https://www.digitalocean.com/community/tutorials/how-to-create-raid-arrays-with-mdadm-on-ubuntu-16-04)

[Arch linux raid wiki](https://wiki.archlinux.org/index.php/RAID)

## LVM

[LVM setup](https://www.digitalocean.com/community/tutorials/how-to-use-lvm-to-manage-storage-devices-on-ubuntu-16-04)



## Compile software

set gcc

```shell
./configure CC=/usr/bin/special-cc
# or
make CC=my_compiler
```

```shell
make -j 4 #set parallel compiling
```



Centos compiling gcc

```shell
yum -y install gmp-devel mpfr-devel libmpc-devel glibc-devel glibc-devel.i686 zip unzip jar

http://mirrors.kernel.org/gnu/gcc/gcc-8.4.0/gcc-8.4.0.tar.gz
tar -zxvf gcc-8.4.0.tar.gz
cd gcc-8.4.0
./configure
make
make install
```

Centos compiling glib-2.14

```shell
# check the system glibc
ldd --version

mkdir ~/glibc_install; cd ~/glibc_install 
wget http://ftp.gnu.org/gnu/glibc/glibc-2.14.tar.gz
tar zxvf glibc-2.14.tar.gz
cd glibc-2.14
mkdir build
cd build
../configure --prefix=/opt/glibc-2.14
make -j 4
sudo make install
export LD_LIBRARY_PATH="/opt/glibc-2.14/lib${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}"
```



## Install software from source

```shell
./configure --prefix=/opt/local
make
make install
```



## Connect to the Server Using SSH Tunneling

```shell
ssh -L server_port:localhost:local_port username@server_ip
```

