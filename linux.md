# Add new volumes

`lsblk` 顯示可用的disk devices

`sudo file -s /dev/xvdf`  
若顯示`/dev/xvdf: data`代表需要建立檔案系統  
`sudo mkfs -t ext4 /dev/xvdf`

接著mount進來  
`sudo mkdir /volume1`  
`sudo mount /dev/xvdf /volume1`
