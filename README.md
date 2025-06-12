<h1 align="center">🏠 Secure Home Office Network Lab 🔒</h1>

<p align="center">
  Este repositório detalha a arquitetura e a implementação da minha infraestrutura de rede e cibersegurança para um ambiente de <strong>home office</strong>. Meu objetivo é demonstrar a aplicação prática de princípios de segurança para proteger uma rede doméstica, otimizar a conectividade e criar um ambiente robusto para trabalho remoto, além de servir como um laboratório de testes para segurança.
</p>

---

<h2 align="center">🛠️ Visão Geral da Arquitetura e Componentes</h2>

<p align="center">Minha configuração foi projetada para oferecer visibilidade, controle e resiliência, utilizando uma combinação estratégica de hardware e software.</p>

### Hardware Base

<ul>
  <li><strong>Computador Host:</strong> Lenovo ThinkCentre M93 Tiny</li>
  <ul>
    <li><em>Função:</em> Servidor compacto e eficiente para hospedar máquinas virtuais.</li>
  </ul>
  <li><strong>Acesso à Internet (WAN):</strong> Modem Aquário 4G Internet Rural</li>
  <ul>
    <li><em>Função:</em> Fornecimento de conectividade primária via rede 4G.</li>
  </ul>
  <li><strong>Roteador Principal:</strong> GL.iNet SFT1200 (Slate AX)</li>
  <ul>
    <li><em>Função:</em> Gerenciamento da rede interna, roteamento e funcionalidades avançadas.</li>
  </ul>
</ul>

### Software e Virtualização

<ul>
  <li><strong>Sistema Operacional Host:</strong> Debian 12</li>
  <ul>
    <li><em>Função:</em> Base estável e segura para a virtualização.</li>
    <li><em>Ferramenta de Virtualização:</em> KVM/libvirt para gerenciamento eficiente das VMs.</li>
  </ul>
  <li><strong>Firewall e Segurança de Borda (VM):</strong> OPNsense</li>
  <ul>
    <li><em>Função:</em> Atua como o principal firewall e gateway de rede, controlando todo o tráfego de entrada e saída.</li>
  </ul>
  <li><strong>Filtragem de DNS e Bloqueio de Ameaças (VM):</strong> Pi-hole</li>
  <ul>
    <li><em>Função:</em> Servidor DNS para toda a rede, responsável por filtrar anúncios, rastreadores e domínios maliciosos.</li>
  </ul>
</ul>

---

<h2 align="center">🔒 Detalhes da Implementação de Segurança</h2>

<p align="center">Esta seção descreve como cada componente contribui para a postura de segurança da rede.</p>

### 1. Firewall e Segmentação com OPNsense

<ul>
  <li><strong>Implementação:</strong> O OPNsense roda como uma máquina virtual dedicada no ThinkCentre M93 Tiny, posicionado estrategicamente como o ponto de entrada e saída da rede local.</li>
  <li><strong>Capacidades Demonstradas:</strong>
    <ul>
      <li><strong>Filtragem Stateful:</strong> Configuração de regras granulares de firewall para permitir ou bloquear tráfego com base em endereços IP, portas, protocolos e estados de conexão.</li>
      <li><strong>Segmentação de Rede:</strong> Criação de VLANs (Virtual Local Area Networks) ou interfaces virtuais para isolar diferentes tipos de dispositivos (ex: rede de trabalho, rede de dispositivos IoT, rede de convidados), minimizando o impacto de uma possível violação.</li>
      <li><strong>Sistema de Prevenção/Detecção de Intrusões (IDS/IPS):</strong> Uso do <strong>Suricata</strong> integrado para monitorar o tráfego em tempo real, identificar padrões de ataque conhecidos e bloquear atividades suspeitas.</li>
      <li><strong>Servidor VPN:</strong> Configuração de servidores VPN (OpenVPN ou WireGuard) para permitir acesso remoto seguro à rede interna ou para tunelar o tráfego de saída da rede através de um serviço VPN externo, garantindo privacidade e segurança em trânsito.</li>
      <li><strong>Gestão de Logs e Auditoria:</strong> Monitoramento e análise de logs para identificar eventos de segurança e auditar o tráfego de rede.</li>
    </ul>
  </li>
</ul>

### 2. Filtragem de DNS e Controle de Conteúdo com Pi-hole

<ul>
  <li><strong>Implementação:</strong> O Pi-hole opera como uma máquina virtual separada no ThinkCentre M93 Tiny, configurado para ser o servidor DNS principal para todos os dispositivos na rede.</li>
  <li><strong>Capacidades Demonstradas:</strong>
    <ul>
      <li><strong>Bloqueio de Malwares e Phishing:</strong> Utilização de listas de bloqueio atualizadas para impedir que os dispositivos acessem domínios conhecidos por hospedar malwares, phishing e outros conteúdos maliciosos.</li>
      <li><strong>Privacidade Aprimorada:</strong> Bloqueio de rastreadores e telemetria de dispositivos, reduzindo a pegada digital e protegendo a privacidade dos usuários da rede.</li>
      <li><strong>Visibilidade de Tráfego DNS:</strong> O dashboard do Pi-hole fornece estatísticas detalhadas sobre as consultas DNS, permitindo identificar padrões de uso, atividades suspeitas e tentativas de acesso a domínios bloqueados.</li>
      <li><strong>Otimização de Desempenho:</strong> Redução da carga de processamento e banda larga ao bloquear requisições para anúncios e outros conteúdos indesejados.</li>
    </ul>
  </li>
</ul>

### 3. Conectividade e Roteamento Otimizado

<ul>
  <li><strong>Modem Aquário 4G Internet Rural:</strong> Fornece a conexão WAN principal, demonstrando adaptabilidade e resiliência em ambientes onde a banda larga fixa pode ser limitada ou indisponível.</li>
  <li><strong>Roteador GL.iNet SFT1200 (Slate AX):</strong>
    <ul>
      <li><strong>Roteamento Eficiente:</strong> Gerencia o tráfego entre a rede local e o OPNsense.</li>
      <li><strong>Flexibilidade:</strong> GL.iNet OS, baseado em OpenWrt, permite configurações avançadas de rede e segurança.</li>
      <li><strong>Cliente VPN:</strong> Pode ser configurado para funcionar como cliente VPN, roteando todo o tráfego da rede através de um túnel seguro para um provedor de VPN, garantindo anonimato e proteção de dados para todos os dispositivos conectados.</li>
    </ul>
  </li>
</ul>

---

<h2 align="center">🎯 Relevância para Cibersegurança em Home Office</h2>

<p align="center">Esta configuração é particularmente relevante para profissionais de cibersegurança e qualquer pessoa que busque um ambiente de trabalho remoto seguro e eficiente, pois oferece:</p>

<ul>
  <li><strong>Defesa em Profundidade:</strong> Múltiplas camadas de segurança (firewall, filtragem DNS) para proteger a rede.</li>
  <li><strong>Controle e Transparência:</strong> Capacidade de monitorar, auditar e gerenciar proativamente o tráfego de rede.</li>
  <li><strong>Privacidade e Anonimato:</strong> Ferramentas para mitigar rastreadores e potencial integração com VPNs.</li>
  <li><strong>Habilidades Práticas:</strong> Demonstra proficiência em virtualização, configuração de firewalls open-source, gerenciamento de DNS e roteamento avançado – competências altamente valorizadas no mercado de cibersegurança.</li>
  <li><strong>Ambiente de Laboratório:</strong> A setup serve como uma plataforma para testar novas ferramentas, simular ataques e aprimorar continuamente as habilidades de segurança sem impactar redes de produção.</li>
</ul>

---

<h2 align="center">➡️ Próximos Passos e Melhorias Futuras</h2>

<p align="center">Planejo expandir e refinar esta infraestrutura com os seguintes projetos:</p>

<ul>
  <li><strong>Implementação de SIEM (Security Information and Event Management):</strong> Configuração de uma solução como ELK Stack (Elasticsearch, Logstash, Kibana) ou Splunk Free para centralizar e analisar logs de todos os dispositivos de segurança.</li>
  <li><strong>Configuração de Honeypots:</strong> Implantação de honeypots para atrair e analisar tentativas de ataque, obtendo inteligência sobre ameaças.</li>
  <li><strong>Automação de Tarefas de Segurança:</strong> Desenvolvimento de scripts (Python/Bash) para automatizar a coleta de logs, alertas e outras rotinas de segurança.</li>
  <li><strong>Testes de Vulnerabilidade:</strong> Realização periódica de varreduras de vulnerabilidade e testes de intrusão na própria rede para identificar e corrigir possíveis falhas.</li>
  <li><strong>Documentação Detalhada:</strong> Criar documentação mais aprofundada para cada serviço, incluindo diagramas de rede mais complexos e guias de configuração passo a passo.</li>
</ul>

---
<h2 align="center">📞 Contato</h2>

<p align="center">Fique à vontade para entrar em contato para discutir este projeto, colaborar ou explorar oportunidades na área de cibersegurança.</p>


<p align="center"> <a href="https://www.linkedin.com/in/julio-melgaco-a80aa7277" target="_blank">
  <img src="https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin" alt="LinkedIn"></p>

</body>
</html>
