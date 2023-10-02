# rpcclient

% rpcclient, rpc, windows

## rpcclient - enumdomusers (Enumeração de usuários de domínio)
#plateform/linux #target/remote #cat/RECON 
```
rpcclient <ip> -U "<user>%<password>" -c "enumdomusers;quit"
```

## rpcclient - srvinfo (Informações do servidor)
#plateform/linux #target/remote #cat/RECON 
```
rpcclient <ip> -U "<user>%<password>" -c "srvinfo;quit"
```

## rpcclient - Obter SID do usuário.
#plateform/linux #target/remote #cat/RECON 
```
rpcclient <ip> -c "lookupnales <name>; wmic useraccount get name,sid; quit"
```

## rpcclient - querydominfo (Obter informações do domínio)
#plateform/linux #target/remote #cat/RECON 
```
rpcclient <ip> -U "<user>%<password>" -c "querydominfo;quit"
```

## rpcclient - getdompwinfo (politica de senhas)
#plateform/linux #target/remote #cat/RECON 
```
rpcclient <ip> -U "<user>%<password>" -c "getdompwinfo;quit"
```

## rpcclient - netshareenum  (politica de senhas)
#plateform/linux #target/remote #cat/RECON 
```
rpcclient <ip> -U "<user>%<password>" -c "netshareenum;quit"
```

## Testa todos usuarios como senhas derivados de uma lista de usuarios.
#plateform/linux #target/remote #cat/ATTACK/BRUTEFORCE-SPRAY  
```
for u in `cat <file>`; do echo -n "user: $u " && rpcclient -U "$u%$u" -c "getusername;quit" <ip>; done
```

## rpcclient - enum (Enum lista de comandos)
#plateform/linux #target/remote #cat/RECON
```
rpcclient <ip> -U "<user>%<pass>" -c "enum;quit"
```

## rpcclient - enumdomains (Dominio atual)
#plateform/linux #target/remote #cat/RECON
```
rpcclient <ip> -U "<user>%<pass>" -c "enumdomains;quit"
```

## rpcclient - enumdomgroups (Enumeração de grupos de domínio)
#plateform/linux #target/remote #cat/RECON
```
rpcclient <ip> -U "<user>%<pass>" -c "enumdomgroups;quit"
```
## rpccliet - querygroup (Enumeração de informações do grupo)
#plateform/linux #target/remote #cat/RECON
```
rpcclient <ip> -U "<user>%<pass>" -c "querygroup <RID>;quit"
```
## rpcclient - querygroupmem (Enumeração de membros do grupo)
#plateform/linux #target/remote #cat/RECON
```
rpcclient <ip> -U "<user>%<pass>" -c "querygroupmem <RID>;quit"
```

## rpccliet - queryuser (Enumeração de informações de um usuario/computador especifico pelo RID)
#plateform/linux #target/remote #cat/RECON
```
rpcclient <ip> -U "<user>%<pass>" -c "queryuser <RID>;quit"
```

## rpccliet - getusrdompwinfo (Política de senha do usuário)
#plateform/linux #target/remote #cat/RECON
```
rpcclient <ip> -U "<user>%<pass>" -c "getusrdompwinfo <RID>;quit"
```

## rpcclient - lsaenumsid (Enumeração de SID utilizando usuários locais LSA)
#plateform/linux #target/remote #cat/RECON
```
rpcclient <ip> -U "<user>%<pass>" -c "lsaenumsid;quit"
```

## rpcclient - lookupsid (Pesquisa de SID de usuários locais)
#plateform/linux #target/remote #cat/RECON
```
rpcclient <ip> -U "<user>%<pass>" -c "lookupsid <SID>;quit"
```

## rpcclient - setuserinfo2 (Reseta a senha do usuario do AD)
#plateform/linux #target/remote #cat/EXPLOIT
```
rpcclient <ip> -U "<user>%<pass>" -c "setuserinfo2 <LOGIN> 23 '<NEWPASSWORD>';quit"
```

