## Maszyny Linux

| VM | Rola |
|---|---|
| `RockyGUIAnsible` | maszyna administracyjna z Ansible |
| `RockyZabbix` | Zabbix Server, PostgreSQL i panel webowy |
| `RockyVPN` | Tailscale |
| `gitlab01` | GitLab CE i Container Registry |
| `jenkins01` | Jenkins Controller |
| `build01` | Jenkins Agent, Docker, Trivy i kubectl |
| `k3s01`–`k3s03` | trzy serwery K3s z embedded etcd |
| `vault01` | HashiCorp Vault |
