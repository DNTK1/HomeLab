# Usługi

| Maszyna       | System                | Usługi                             |
| ------------- | --------------------- | ---------------------------------- |
| OPNsense      | OPNsense              | Router, firewall i DNS dla sieci   |
| DC01          | Windows Server 2025   | Active Directory, DNS, DHCP        |
| DC02          | Windows Server 2025   | Drugi kontroler domeny, DNS, DHCP  |
| ROOTCA01      | Windows Server 2025   | Główny urząd certyfikacji, offline |
| ISSUINGCA01   | Windows Server 2025   | Wydawanie certyfikatów i IIS       |
| FileserverSMB | Rocky Linux 10           | Udział plików Samba                |
| PBS           | Proxmox Backup Server | Kopie zapasowe VM                  |
| ANSIBLE01     | Rocky Linux 10           | Ansible i Kubespray                |
| CP01–CP03     | Rocky Linux 10           | Kubernetes control plane i etcd    |
| WK01–WK03     | Rocky Linux 10           | Workery Kubernetes                 |

## Active Directory

DC01 i DC02 obsługują jedną domenę. Oba serwery mają DNS i DHCP. GPO służą między innymi do rozsyłania certyfikatu i automatycznego wydawania certyfikatów kontrolerom domeny.

## PKI

ROOTCA01 jest odłączony od sieci. ISSUINGCA01 wydaje certyfikaty dla usług. IIS udostępnia certyfikaty urzędów i listy unieważnionych certyfikatów.

## Pliki i backup

Samba przechowuje pliki oraz obrazy instalacyjne. Proxmox Backup Server przechowuje kopie VM na osobnym dysku HDD.

## Kubernetes

Klaster został wdrożony przez Kubespray na sześciu fizycznych mini PC Lenovo M710q. CP01, CP02 i CP03 obsługują control plane i etcd. WK01, WK02 i WK03 uruchamiają aplikacje.