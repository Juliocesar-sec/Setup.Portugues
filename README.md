<h1 align="center">🏠 Secure Home Office Network Lab 🔒</h1>

<p align="center">
  Este repositório detalha a arquitetura e a implementação da minha infraestrutura de rede e de cibersegurança para um ambiente de <strong>home office</strong>. Meu objetivo é demonstrar a aplicação prática de princípios de segurança para proteger uma rede doméstica, otimizar a conectividade e criar um ambiente robusto de trabalho remoto, além de funcionar como um laboratório de testes em segurança da informação.
</p>

---

# 🔒 Projeto: Laboratório de Segurança e Rede com pfSense + Suricata + Squid

## 📡 Estrutura de Rede

**Hypervisor:** VirtualBox  
**Firewall:** pfSense  
**Interfaces de rede configuradas:**

| Interface   | Tipo          | Finalidade                          |
|-------------|---------------|--------------------------------------|
| Adapter 1   | NAT           | Acesso externo (WAN)                |
| Adapter 2   | Host-only     | Administração local (LAN)           |
| Adapter 3   | Internal Network | Rede interna de clientes (OPT1)  |

---

## ⚙️ Configurações no pfSense

### Interfaces
- **WAN:** DHCP via NAT
- **LAN:** `192.168.56.1/24` (host-only)
- **OPT1:** `192.168.50.1/24` (clientes internos)

### DHCP (em OPT1)
- **Faixa:** `192.168.50.100 – 192.168.50.200`
- **Servidores DNS:**
  - `192.168.50.1` (pfSense)
  - `8.8.8.8`, `1.1.1.1` (externos)

### Regras de Firewall
- Permitir: `OPT1 subnet -> any`
- Logging: **ativado** para debug

---

## 🛡️ Suricata IDS/IPS

### Instalação
- Realizada via **System > Package Manager**

### Interface Monitorada
- `OPT1` (rede interna)

### Configuração
- **Modo:** Inline IPS
- **Block Offenders:** ✔️
- **Auto-enable Flowbits:** ✔️
- **Pass List criada:** `rede-confiavel`

#### Pass List (IPs confiáveis)
- `192.168.50.1` → gateway pfSense
- `192.168.56.1` → host físico
- `8.8.8.8`, `1.1.1.1` → DNS externos

### Categorias de Regras Ativadas (exemplos)
- `emerging-malware.rules`
- `emerging-botcc.rules`
- `emerging-exploit.rules`
- `stream-events.rules`
- `dns-events.rules`
- `http-events.rules`

---

## 🌐 Squid Proxy

### Modo: Transparent Proxy
- Interface: `OPT1`
- Proxy intercepta requisições HTTP automaticamente
- HTTPS: **não interceptado** (SSL Bump desativado por padrão)

### ACLs
- Subrede permitida: `192.168.50.0/24`
- Cache local: ativado (100MB)

### Logs
- Local: `/var/squid/logs/access.log`
- GUI: `Status > System Logs > Proxy`

---

## ✅ Testes Realizados

- Acesso a sites HTTP e HTTPS via proxy
- Teste do Suricata com `curl http://testmyids.com`
- Bloqueios e desbloqueios com base em regras do Suricata
- Verificação de logs (proxy e IDS)
- DHCP funcional e clientes com navegação sem configuração manual
- Pass List protegendo IPs internos de bloqueios do IPS

---

## 📌 Extensões Futuras

- [ ] SquidGuard: filtro por categoria
- [ ] Lightsquid: relatórios gráficos de acesso
- [ ] SSL Bump: interceptação e inspeção HTTPS
- [ ] pfBlockerNG: GeoIP, IP reputation, ASN
- [ ] Autenticação de usuários no proxy

---

## 🗂 Estrutura do Repositório

/
├── README.md
├── pfsense_config/
│ ├── firewall_rules.txt
│ ├── passlist_conf.txt
│ ├── squid_conf_summary.txt
├── logs/
│ ├── squid_access_sample.log
│ ├── suricata_alerts.log
└── notes/
└── extensions_plan.md


---

## 👨‍💻 Autor

> Laboratório pessoal para estudo e implementação prática de segurança em redes usando pfSense, Suricata e Squid Proxy. Ideal para aprender IDS/IPS, firewall, proxy transparente e controle de tráfego em ambientes isolados.

---

<h2 align="center">📞 Contato</h2>

<p align="center">Fique à vontade para entrar em contato para discutir este projeto, colaborar ou explorar oportunidades na área de cibersegurança.</p>

<p align="center">
  <a href="https://www.linkedin.com/in/julio-melgaco-a80aa7277" target="_blank">
    <img src="https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin" alt="LinkedIn">
  </a>
</p>
