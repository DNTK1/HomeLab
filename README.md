# HomeLab

Projekt ma na celu naukę i eksperymentowanie/troubleshooting w środowisku zbliżonym do firmowego. Całość jest oparta na klastrze 3 nodów z Proxmox VE + Ceph oraz 6 nodach z Rocky Linux pod klaster Kubernetesa (3 control plane, 3 workery). Dodatkowo osobny host służy jako router/firewall z OPNsensem.

## Usługi

| Usługa                       | Zastosowanie                                                                   |
| ---------------------------- | ------------------------------------------------------------------------------ |
| Proxmox VE + Ceph            | Wirtualizacja i wspólne miejsce na dyski VM                                    |
| Kubernetes                   | Klaster wdrożony przez Kubespray, containerd, Calico VXLAN i kube-vip          |
| OPNsense                     | Routing między VLAN-ami, firewall, NAT i Unbound DNS                           |
| Active Directory, DNS i DHCP | Domena Windows i usługi sieciowe na dwóch kontrolerach                         |
| PKI                          | Offline Root CA i domenowy Issuing CA, publikacja certyfikatów i CRL przez IIS |
| Samba                        | Udział plików i obrazy instalacyjne                                            |
| Proxmox Backup Server        | Kopie zapasowe VM                                                              |
| Ansible                      | Zarządzanie hostami Linux i wdrożenie Kubernetes                               |

## Dokumentacja

| Katalog | Zawartość |
|---|---|
| [infra](infra/README.md) | Sprzęt, Proxmox, dyski i sieć |
| [services](services/README.md) | Usługi Windows, Linux i Kubernetes |
| [ansible](ansible/README.md) | Zarządzanie hostami Linux i Kubespray |
