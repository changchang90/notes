---
layout: post
title: "利用 Netplan 設定網路"
date: 2018-06-11 22:00:00 +0800
categories: 
  - Ubuntu
tags:
  - network
  - netplan
---

自 Ubuntu 16.10 可以使用 Netplan 設定網路，在 Ubuntu 18.04 LTS (Bionic Beaver) 則將 Netplan作為預設的網路設定套件，就來學學怎麼配置吧。

### 使用語法
Netplan 使用 YAML 格式撰寫，關於 YAML 可以參考[維基百科-YAML](https://zh.wikipedia.org/wiki/YAML)。

### 設定檔位置
安裝完 Ubuntu 18.04 後，編輯 /etc/netplan/01-netcfg.yaml 來修改網路配置。你也可以在這麼資料夾新增 02-XXX.yaml 來進行額外的網路設定。

### 設定 IPv4 DHCP
在 ens3 這個網路介面上設定 IPv4 DHCP。
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    ens3:
      dhcp4: yes
```

### 手動設定 IPv4 位址 (Static IP)
在 ens3 這個網路介面上設定 IPv4 位址，並指定 Gateway 與 DNS Server。
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    ens3:
      addresses:
        - 192.168.1.2
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]
```

### 套用網路設定
* 你可以選擇重開機。
* 你也可使利用指令，並檢查你的設定檔是不是有錯誤。
```bash
sudo netplan apply
```

### 參考
1. [Ubuntu Wiki - Netplan Design](https://wiki.ubuntu.com/Netplan/Design)
2. [Ubuntu Blog - Ubuntu Bionic: Netplan](https://blog.ubuntu.com/2017/12/01/ubuntu-bionic-netplan)