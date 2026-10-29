# Lab SOC/Blue Team — do zero ao primeiro incidente detectado

Repositório onde documento a montagem de um home lab de segurança focado em SOC/Blue Team, do absoluto zero até os primeiros exercícios de detecção. Faz parte da minha transição de carreira de TI/Infraestrutura para Cibersegurança.

## Objetivo

Construir um ambiente isolado em VirtualBox onde eu possa:
- Simular ataques reais (brute force, movimentação lateral, etc.)
- Detectar esses ataques num SIEM (Wazuh)
- Documentar cada exercício como um mini relatório de incidente — material de portfólio e conteúdo pro LinkedIn

## Arquitetura

```
┌─────────────┐      ataques      ┌──────────────────┐      logs      ┌────────────────┐
│ Kali Linux  │ ────────────────> │  Windows 10/11    │ ─────────────> │  Wazuh Manager  │
│ (atacante)  │                   │  (alvo + Sysmon)  │                │  (SIEM central) │
└─────────────┘                   └──────────────────┘                └────────┬────────┘
                                                                                 │ alertas
                                                                                 ▼
                                                                          ┌────────────┐
                                                                          │    Eu      │
                                                                          │ (dashboard)│
                                                                          └────────────┘
```

Todas as VMs ficam numa **Rede Interna** isolada do VirtualBox (`labsoc`), sem acesso à minha rede doméstica.

| Papel | VM | IP planejado |
|---|---|---|
| SIEM | Wazuh Manager (OVA) | 192.168.56.10 |
| Alvo | Windows 10/11 + Sysmon + Agente Wazuh | 192.168.56.20 |
| Atacante | Kali Linux | 192.168.56.30 |

## Roadmap (fases)

- [x] **Fase 1 — VirtualBox + rede interna + Wazuh importado**
  Instalação do VirtualBox, Extension Pack, importação do OVA do Wazuh e configuração da rede interna `labsoc`.
- [ ] **Fase 2 — Configurar o Wazuh**
  Ligar a VM, acessar o dashboard, trocar a senha padrão, ajustar IP fixo.
- [ ] **Fase 3 — VM Windows alvo**
  Criar a VM Windows 10/11, instalar Sysmon (config da SwiftOnSecurity) e o agente Wazuh.
- [ ] **Fase 4 — VM Kali Linux (atacante)**
  Importar e configurar a VM do Kali na mesma rede interna.
- [ ] **Fase 5 — Primeiro exercício prático**
  Brute force de RDP do Kali contra o Windows, detecção do Event ID 4625 no Wazuh, criação de regra de alerta e relatório de incidente.
- [ ] **Expansão**
  Windows Server com AD (Kerberoasting, criação de usuário privilegiado), VM Linux com FIM, pfSense + Suricata (IDS de rede), Atomic Red Team mapeado no MITRE ATT&CK.

## Pré-requisitos

- 16 GB de RAM no host
- 100 GB livres em disco
- Virtualização habilitada na BIOS (Intel VT-x ou AMD-V)

## Downloads

| Item | Link |
|---|---|
| VirtualBox | https://www.virtualbox.org/wiki/Downloads |
| VirtualBox Extension Pack | https://www.virtualbox.org/wiki/Downloads |
| Wazuh OVA | https://documentation.wazuh.com/current/virtual-machine/virtual-machine.html |
| Windows 11 ISO (avaliação, 90 dias) | https://www.microsoft.com/en-us/evalcenter/evaluate-windows-11-enterprise |
| Kali Linux (VM pronta) | https://www.kali.org/get-kali/#kali-virtual-machines |

---

## 🗂️ Projetos

| # | Projeto | Descrição | Área | Status |
|---|---------|-----------|------|--------|
| 01 | [🔭 01 Configuração do VirtualBox](./01-config-das-vms) | configuração do Virtual Box com o Kali Linux, Windows 11 e Wazuh. | Red & Blue Team | Instalação Completa |
| 01 | [🔭 Home Lab de Segurança](./02-Mapeamento-de-REdes) | Laboratório virtual com Ubuntu Linux | Red & Blue Team | Instalação Completa |

> Novos projetos serão adicionados conforme o aprendizado avança. Acompanhe! ⭐

---


## Estrutura do repositório

```
.
├── README.md                      ← este arquivo, visão geral do projeto
├── fase-1-virtualbox-wazuh/
│   ├── README.md                  ← passo a passo detalhado da Fase 1
│   └── Screenshots/                    ← prints
├── fase-2-config-wazuh/
├── fase-3-windows-alvo/
├── fase-4-kali/
└── exercicios/
    └── 01-brute-force-rdp/
        ├── README.md               ← relatório do exercício
        └── assets/                 ← evidências (prints de eventos, regras criadas)
```

Cada fase e cada exercício tem seu próprio README detalhado — este arquivo principal é só o mapa do projeto.

## Status atual

🟢 Fase 1 concluída — VirtualBox, Extension Pack e Wazuh (OVA) importado e na rede interna.
🔜 Próximo passo: Fase 2 — configurar o dashboard do Wazuh.

## Sobre

Projeto de estudo pessoal, parte da minha jornada de transição para SOC/Blue Team. Acompanho e documento o progresso também no [LinkedIn].
