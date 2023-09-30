# impacket

## smbclient - Conecta ao smb do alvo.
#plateform/linux #target/remote #port/445 #protocol/smb #cat/ATTACK/CONNECT  


Um client smb que permite listagem dos shares e arquivos, renomear, upload e download de arquivos, criar ou deletar diretorios, sendo possivel usar as seguintes combinações de autenticação: usuario/senha  ou usuario/hash

-hashes : <LMHASH:NTHASH>
-no-pass -k : kerberos authentication

```
smbclient.py <domain>/<user>:<password>@<ip>
```

