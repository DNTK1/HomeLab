# Infrastruktura

## Sprzęt

| Host                 | Sprzęt                            | RAM   | Dyski                             | Zastosowanie          |
| -------------------- | --------------------------------- | ----- | --------------------------------- | --------------------- |
| Lab1                 | HP EliteDesk 800 G4 SFF, i5-8400T | 32 GB | NVMe 128 GB + NVMe 1 TB           | Proxmox i Ceph        |
| Lab2                 | HP EliteDesk 800 G4 SFF, i5-8500  | 32 GB | NVMe 128 GB + NVMe 1 TB           | Proxmox i Ceph        |
| Lab3                 | HP EliteDesk 800 G4 SFF, i5-8500  | 32 GB | NVMe 256 GB + NVMe 1 TB           | Proxmox i Ceph        |
| LabFirewall          | HP EliteDesk 800 G3 SFF, i5-6500  | 16 GB | NVMe 256 GB, SSD 500 GB, HDD 2 TB | OPNsense, Samba i PBS |
| CP01–CP03, WK01–WK03 | 6 × Lenovo M710q Tiny             | 8GB   | NVMe 128 GB                       | Rocky Linux           |

## Proxmox i dyski

Lab1, Lab2 i Lab3 tworzą klaster EILAB. Każdy ma osobny dysk pod system i NVMe dla Cepha.

LabFirewall działa poza klastrem. Jego maszyny korzystają z lokalnych dysków. SSD 500 GB jest przeznaczony na pliki Samby, a HDD 2 TB na backupy PBS.

| Storage | Zastosowanie |
|---|---|
| local-lvm | Lokalne dyski VM |
| ceph-vm | Wspólne dyski VM w klastrze |
| FileserverSMB | Obrazy ISO i cloud |
| PBS | Kopie zapasowe VM |

## Sieć

OPNsense obsługuje dostęp do Internetu i ruch między VLAN-ami.

| VLAN          | Zastosowanie                    |
| ------------- | ------------------------------- |
| 10_MGMT       | Zarządzanie hostami i switchami |
| 20_SERVERS    | VM Windows i Linux              |
| 30_ADMIN      | Komputer administracyjny        |
| 40_BACKUP     | Ruch do PBS                     |
| 50_K8S        | Hosty Lenovo                    |
| 60_CLIENTS    | Komputery testowe               |
| 70_AUTOMATION | Ansible                         |

Trzy switche łączą hosty i urządzenia w labie:

| Switch | Model | Porty |
|---|---|---|
| CORE | ZX310S-8T2XS | 8 × 2,5 Gb/s, 2 × SFP+ 10 Gb/s |
| SW-MGMT | Horaco HC-SWTGW218AS | 8 × 2,5 Gb/s, 1 × SFP+ 10 Gb/s |
| SW-K8S | Horaco HC-SWTGW218AS | 8 × 2,5 Gb/s, 1 × SFP+ 10 Gb/s |

Ceph korzysta z osobnych połączeń 10 Gb/s. Każdy host jest połączony bezpośrednio z dwoma pozostałymi. Routing między nimi obsługuje FRR z OSPF. MTU 1500 - nie było potrzeby podnosić, transfery 9,4-9,5Gbit/s.
