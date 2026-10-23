# 🔍 Projeto 02 — Mapeamento de Rede com Nmap

## 🎯 Objetivo

Utilizar o **Nmap** para escanear uma rede interna e descobrir hosts ativos, portas abertas e serviços em execução — simulando a fase de **reconhecimento** de um processo real de pentest.

---

## 🖥️ Ambiente

![Kali Linux](https://img.shields.io/badge/Kali_Linux-557C94?style=for-the-badge&logo=kali-linux&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![VirtualBox](https://img.shields.io/badge/VirtualBox-183A61?style=for-the-badge&logo=virtualbox&logoColor=white)
![Nmap](https://img.shields.io/badge/Nmap-214478?style=for-the-badge&logoColor=white)

| Máquina | Sistema | IP | Papel |
|---------|---------|-----|-------|
| VM 1 | Kali Linux | 192.168.0.20 | Atacante (scanner) |
| VM 2 | Ubuntu Server | 192.168.0.14 | Alvo |

> As duas VMs foram conectadas via **Rede Interna (LabSec)** no VirtualBox, criando um ambiente isolado e seguro para os testes.

---

## ⚙️ Configuração da Rede

Antes de rodar o Nmap, foi necessário configurar os IPs manualmente nas duas VMs, pois a rede interna do VirtualBox não possui DHCP automático.

**No Ubuntu Server (alvo):**
```bash
sudo ip addr add 192.168.0.14/24 dev enp0s3
ip a  # confirmar o IP
