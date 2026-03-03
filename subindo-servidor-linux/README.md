# Estudo de Caso 1: Hardening e Configuração de Infraestrutura Linux

Este repositório documenta a implementação de uma camada de segurança e administração em um servidor Linux do zero. O projeto foi desenvolvido como um desafio prático proposto pelo [roadmap.sh](https://roadmap.sh/projects/linux-server-setup), focando em transformar uma instância "nua" em um ambiente preparado para produção.

---

## 📖 Contexto

Ao provisionar um servidor na nuvem (VPS ou aqui uma VM Local), a configuração padrão precisa de algumas mudanças para ficarem mais seguras e otimizadas: acesso via usuário root, autenticação por senha e portas abertas. Este estudo de caso detalha a estratégia utilizada para mitigar esses riscos, estabelecendo uma base sólida de segurança antes da implantação de qualquer aplicação.

> 🎥 **Estudo de Caso Aplicado em vídeo:** [Link para seu vídeo aqui]

---

## 🎯 Objetivos Estratégicos

O projeto foi estruturado em quatro pilares fundamentais:

### 1. Gestão de Identidade e Acesso (IAM)
A primeira barreira de defesa foi eliminar o uso do usuário `root`. 
- **Finalidade:** Implementar o princípio do privilégio mínimo. Ao criar um usuário comum com poder de `sudo` sob demanda, reduzimos as chances de comandos acidentais ou ataques que comprometam todo o sistema instantaneamente.

### 2. Endurecimento do Acesso Remoto (SSH)
Substituímos a autenticação por senha pelo uso de **Chaves Criptográficas (SSH Keys)**.
- **Finalidade:** Tornar ataques de força bruta virtualmente impossíveis. Com a desativação da senha e do login de root no arquivo de configuração do daemon SSH, o servidor só responde a quem possui a chave privada autorizada.

### 3. Defesa de Perímetro e Monitoramento Ativo
Implementação de firewall e ferramentas de banimento automático.
- **UFW (Uncomplicated Firewall):** Configurado para uma política de *Default Deny* (bloquear tudo por padrão), permitindo apenas o tráfego essencial.
- **Fail2Ban:** Atua como um sistema de prevenção de intrusão, monitorando logs em tempo real e banindo temporariamente IPs que demonstrem comportamento malicioso.

### 4. Manutenção e Resiliência
- **Unattended-Upgrades:** Configuração de patches de segurança automáticos para garantir que o kernel e bibliotecas críticas estejam sempre protegidos contra vulnerabilidades conhecidas (CVEs).
- **Padronização de Ambiente:** Ajuste de Hostname e Timezone para garantir que os logs do sistema sejam precisos e fáceis de auditar em caso de incidentes.

---

## 🧠 Competências

* **Administração de Sistemas:** Gerenciamento de usuários, grupos e permissões.
* **Segurança de Rede:** Configuração de regras de filtragem de pacotes.
* **Automação de Manutenção:** Garantia de que o servidor "se cuide" sozinho em relação a atualizações críticas.
* **Auditoria:** Uso de `journalctl` e inspeção de logs em `/var/log/` para diagnóstico de saúde do servidor.

---

## 🛠️ Tecnologias Utilizadas

* **SO:** Ubuntu Server (LTS)
* **Firewall:** UFW
* **Segurança:** Fail2Ban, SSH (RSA/Ed25519), Unattended-Upgrades
* **Monitoramento:** Systemd (Systemctl / Journalctl)

---

## 📝 Créditos
Este projeto é uma implementação do desafio prático de [Linux Server Setup](https://roadmap.sh/projects/linux-server-setup) do **roadmap.sh**.
