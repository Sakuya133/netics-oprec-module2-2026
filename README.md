<img width="1505" height="925" alt="Screenshot_20260331_210031" src="https://github.com/user-attachments/assets/2858967d-bb5f-4543-952d-be475aff15d7" />

# netics-oprec-module2-2026

## 1.​ Lakukan instalasi Wazuh Manager pada sebuah VM/VPS berbasis Linux
(dianjurkan Ubuntu/Debian).

## Penjelasan
<p>Disini saya melakukan instalasi wazuh pada vps menggunakan command quicksetup </p>

```sh
sudo bash wazuh-install.sh -a 
```

## Hasil

<img width="1505" height="925" alt="Screenshot_20260331_210031" src="https://github.com/user-attachments/assets/eccf80e7-a19d-422b-a0cd-5cea3a9be21f" />
<img width="1508" height="910" alt="Screenshot_20260331_210101" src="https://github.com/user-attachments/assets/2b09a01a-b594-4335-9f87-f70a3a10b3e1" />


## Referensi
https://documentation.wazuh.com/current/quickstart.html

## 2.​ Lakukan instalasi Wazuh Agent pada satu perangkat lain, bebas
menggunakan sistem operasi Windows atau Linux.

## Penjelasan
<p>Disini saya buat agent pertama melalui wazuh dashboard, untuk agentnya saya menggunakan vps lain, dengan 1 cpu dan 1 ram </p>

## Hasil
<img width="1397" height="444" alt="image" src="https://github.com/user-attachments/assets/93a4ebb3-29ab-4f9f-8a2f-b9a8f9c6b3e4" />



## Referensi
https://documentation.wazuh.com/current/installation-guide/wazuh-agent/index.html


## 3.​ Pastikan agent berhasil terhubung ke manager dengan mengecek apakah
default events/logs dari agent sudah masuk dan terlihat di dashboard
Wazuh.

## Penjelasan 
<p>Setelah berhasil kita coba check pada sisi agent apakah sudah tersambung, bisa di check pada bagian wazuh dashboard</p>

<img width="1913" height="593" alt="image" src="https://github.com/user-attachments/assets/0666d1c2-dd69-4aa9-ad8f-b725e357207c" />


## Referensi
https://documentation.wazuh.com/current/installation-guide/wazuh-agent/index.html


## 4.​ Buat/mencari dan implementasikan minimal 5 custom rules/custom alert
pada agent kalian. Jenis rules bebas dan dapat menyesuaikan
kreativitas serta konteks keamanan masing-masing. Maksimal rules
tidak dibatasi, lebih banyak lebih baik.

## Penjelasan 
<p>Pada wazuh manager di vps, kita cari file ini  </p>

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

### Custom Rules

```xml
<group name="sshd,sudo,account,">

  <rule id="100100" level="10" frequency="2" timeframe="120">
    <if_matched_sid>5710</if_matched_sid>
    <same_srcip />
    <description>nyoba ssh lagi lagi</description>
    <mitre>
      <id>T1110</id>
    </mitre>
    <group>authentication_failed,invalid_login,bruteforce,</group>
  </rule>

  <rule id="100101" level="14">
    <if_sid>5715</if_sid>
    <user>root</user>
    <description>login root njir</description>
    <mitre>
      <id>T1078</id>
    </mitre>
    <group>authentication_success,root_login,</group>
  </rule>

  <rule id="100102" level="10">
  <if_sid>5404</if_sid>
  <description>bro ngebrute force </description>
  <mitre>
    <id>T1548.003</id>
  </mitre>
  <group>authentication_failed,privilege_escalation,sudo_failed,</group>
</rule>


  <rule id="100103" level="13">
  <if_sid>5402</if_sid>
  <description>root beraksi</description>
  <mitre>
    <id>T1548.003</id>
  </mitre>
  <group>privilege_escalation,command_execution,</group>
</rule>

  <rule id="100104" level="11">
    <program_name>useradd</program_name>
    <match>new user</match>
    <description>ada user baru?</description>
    <mitre>
      <id>T1136</id>
    </mitre>
    <group>account_management,persistence,user_creation,</group>
  </rule>

  <rule id="100105" level="8">
    <program_name>passwd</program_name>
    <match>password changed</match>
    <description>password ganti cik</description>
    <mitre>
      <id>T1098</id>
    </mitre>
    <group>account_management,credential_access,password_change,</group>
  </rule>
  

<rule id="100106" level="10">
  <if_sid>5501</if_sid>
  <description>pam: User session opened.</description>
  <group>authentication_success,login,</group>
</rule>
</group>
```

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

### Flow Diagram
<img width="1020" height="550" alt="image" src="https://github.com/user-attachments/assets/1c33f1bd-a134-4677-9737-284a0aa99370" />

