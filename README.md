# Hacking
SMB Ethical Hacking Lab: Brute Force &amp; Credential Analysis

Este repositório contém os recursos e a metodologia técnica utilizada para executar um cenário de ataque controlado ao protocolo SMB (Server Message Block). O foco principal é demonstrar como vulnerabilidades de configuração e senhas fracas podem ser exploradas, utilizando o Kali Linux como atacante e o Metasploitable 2 como alvo (IP: 10.0.0.2).

🛠️ Tecnologias e Ferramentas
SO Atacante: Kali Linux

SO Alvo: Metasploitable 2 (Linux-based)

Linguagem: Python 3 (Geração de Wordlists)

Ferramentas: Medusa, nmap, smbclient e enum4linux.

📜 Visão Crítica: Infraestrutura Real vs. Laboratório
Como profissional com mais de 20 anos de experiência em Linux (desde 2005), este laboratório serve para validar conceitos fundamentais. No entanto, é vital notar que ambientes modernos (Debian 12/13, Rocky Linux) possuem defesas que tornam ataques genéricos obsoletos:

EDR/IPS: Bloqueiam ataques de força bruta paralelos rapidamente.

MFA: Invalida a posse apenas da senha.

SMB Signing: Impede ataques de relay e interceptação.

🚀 O Desafio Técnico
1. Preparação da Wordlist Inteligente
Em vez de utilizar listas massivas e ineficientes, utilizei um script Python customizado para gerar combinações baseadas em padrões corporativos e contexto do alvo.

Script: gen_wordlist.py

Python
# Execução:
python3 gen_wordlist.py
2. Reconhecimento (Footprinting)
Identificação do serviço no alvo 10.0.0.2:

Bash
nmap -p 445 --script smb-os-discovery 10.0.0.2
3. Execução do Ataque (Medusa)
Uso do Medusa para testar as credenciais geradas de forma paralela no módulo smbnt:

Bash
medusa -h 10.0.0.2 -U custom_users.txt -P custom_pass.txt -M smbnt
4. Validação e Exploração
Após a obtenção de credenciais válidas, a validação de acesso aos diretórios foi feita via smbclient:

Bash
smbclient -L //10.0.0.2/ -U [USER]
🛡️ Mitigação e Boas Práticas
Para proteger infraestruturas modernas contra este tipo de vetor:

Implementar políticas rígidas de Account Lockout.

Desativar protocolos legados (SMBv1).

Monitorar logs de autenticação falha via SIEM.

👨‍💻 Sobre o Autor
Especialista em TI com longa trajetória em administração de servidores Linux, infraestrutura de redes e segurança. Experiência consolidada em migrações complexas de ambientes Windows para Linux e arquitetura Cloud.
