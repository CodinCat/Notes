# OpenSSL

Create a self-signed certificate:

```sh
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365
```

Decrypt the private key:

```sh
openssl rsa -in key.pem -out decrypted_key.pem
```

# Add new volumes

`lsblk` 顯示可用的disk devices

`sudo file -s /dev/xvdf`  
若顯示`/dev/xvdf: data`代表需要建立檔案系統  
`sudo mkfs -t ext4 /dev/xvdf`

接著mount進來  
`sudo mkdir /volume1`  
`sudo mount /dev/xvdf /volume1`

### Make it permanent

`sudo vim /etc/fstab`  
`/dev/xvdf   /volume1   ext4   defaults,nofail   0   2`  

# Swap

`sudo fallocate -l 4G /swapfile`  
`sudo chmod 600 /swapfile`  
`sudo mkswap /swapfile`  
`sudo swapon /swapfile`  

### Make it permanent

`sudo vim /etc/fstab`  
`/swapfile   none    swap    sw    0   0`  

# Misc

#### 把資料夾底下包含子資料夾內的所有檔案，搬移到另一個資料夾根目錄

`find ~/folder1/ -type f -print0 | xargs -0 mv -t ~/folder2`

#### 把除了某類型以外的所有檔案刪除

`find . -type f ! -name '*.txt' -delete`
