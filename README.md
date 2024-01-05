# 🐧Alpine

## 📚`SMB`挂载
```
apk add cifs-utils
mount -t cifs //<smb_ip>/data /smb -o user=<smb_user>
```
> [开机自动挂载](https://blog.gazer.win/essay/cifs-netmount-on-alpine-linux.html)
```bash
apk add cifs-utils openrc
sudo rc-update add netmount

cat >> /etc/fstab << EOF
//10.1.1.1/share.dir /opt/mount.point cifs  _netdev,credentials=/root/.smb.auth,gid=1000,uid=1000,dynperm,exec,noacl,nobrl,nofail,nounix,rw,serverino,setuids,sfu 0 0
EOF


cat > /root/.smb.auth << EOF
username=username
password=password
domain=doaminname
EOF

chmod 600 /root/.smb.auth
# 初次手动挂载(免重启)
mount -a
```
## 💿新硬盘挂载
```bash
> 查看所有硬盘
fdisk -l
```
> 硬盘分区
```bash
fdisk /dev/sda
```
> g 创建GPT分区表
> w 保存配置

> 格式化硬盘
```bash
mkfs -t ext4 /dev/sda
```
> 创建目录挂载硬盘
```bash
mkdir /storage
mount /dev/sda /storage
```
> 修改/etc/fstab
```bash
/dev/sda   /storage    ext4   defaults  0 0
```
