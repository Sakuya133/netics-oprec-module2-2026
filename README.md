# netics-oprec-module2-2026

## 1.​ Lakukan instalasi Wazuh Manager pada sebuah VM/VPS berbasis Linux
(dianjurkan Ubuntu/Debian).

## Penjelasan
<p>Disini saya melakukan instalasi wazuh pada vps menggunakan command quicksetup </p>

```sh
sudo bash wazuh-install.sh -a 
```

## Hasil

``
``

## Referensi
https://documentation.wazuh.com/current/quickstart.html

## 2.​ Lakukan instalasi Wazuh Agent pada satu perangkat lain, bebas
menggunakan sistem operasi Windows atau Linux.

## Penjelasan
<p>Disini saya buat agent pertama melalui wazuh dashboard, untuk agentnya saya coba 2 agent satunya linux dan satunya lagi windows (pinjam pc lab)</p>

## Hasil


## Referensi
https://documentation.wazuh.com/current/installation-guide/wazuh-agent/index.html


## 3.​ Pastikan agent berhasil terhubung ke manager dengan mengecek apakah
default events/logs dari agent sudah masuk dan terlihat di dashboard
Wazuh.

## Penjelasan 
<p>Setelah berhasil kita coba check pada sisi agent apakah sudah tersambung</p>




## Referensi
https://documentation.wazuh.com/current/installation-guide/wazuh-agent/index.html


## 4.​ Buat/mencari dan implementasikan minimal 5 custom rules/custom alert
pada agent kalian. Jenis rules bebas dan dapat menyesuaikan
kreativitas serta konteks keamanan masing-masing. Maksimal rules
tidak dibatasi, lebih banyak lebih baik.

## Penjelasan 
<p>Pada wazuh manager di vps  </p>

```sh
/var/ossec/etc/rules/local_rules.xml
```

<p>Jika kita coba cat akan ada template</p>

```xml
root@vps-netics:/var/ossec/etc/rules# cat local_rules.xml
<!-- Local rules -->

<!-- Modify it at your will. -->
<!-- Copyright (C) 2015, Wazuh Inc. -->

<!-- Example -->
<group name="local,syslog,sshd,">

  <!--
  Dec 10 01:02:02 host sshd[1234]: Failed none for root from 1.1.1.1 port 1066 ssh2
  -->
  <rule id="100001" level="5">
    <if_sid>5716</if_sid>
    <srcip>1.1.1.1</srcip>
    <description>sshd: authentication failed from IP 1.1.1.1.</description>
    <group>authentication_failed,pci_dss_10.2.4,pci_dss_10.2.5,</group>
  </rule>

</group>
root@vps-netics:/var/ossec/etc/rules# 
```
<p>Disinilah sandbox kita dimulai</p>

## Hasil


## 5.​ Buat sebuah dokumentasi penjelasan bagaimana kalian menyelesaikan
penugasan modul 2 ini termasuk Langkah instalasi manager dan agent,
flow/diagram visualisasi deployment, validasi koneksi agent-manager,
penjelasan
 masing-masing
 custom
 rule
 yang
 ditambahkan,
 dan
screenshot hasil dari dashboard/alert yang menunjukkan rules
tersebut aktif pada Github repository kalian.
