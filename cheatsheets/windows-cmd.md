# Cheatsheet Windows CMD

Referencia rápida de comandos clásicos de Windows CMD.

---

## Sistema

```cmd
hostname
whoami
ver
systeminfo
date /t
time /t
```

---

## Archivos y carpetas

```cmd
dir
cd C:\Ruta
mkdir carpeta
rmdir carpeta
type archivo.txt
copy origen destino
xcopy origen destino /E /I
robocopy origen destino /E
move origen destino
del archivo.txt
```

---

## Búsqueda y texto

```cmd
find "texto" archivo.txt
findstr "texto" archivo.txt
findstr /S /I "error" *.log
```

---

## Procesos

```cmd
tasklist
tasklist | findstr notepad
taskkill /PID 1234
taskkill /IM notepad.exe /F
```

---

## Servicios

```cmd
sc query
sc query Spooler
sc start Spooler
sc stop Spooler
net start
net start Spooler
net stop Spooler
```

---

## Usuarios y grupos

```cmd
net user
net user usuario contraseña /add
net user usuario /delete
net localgroup
net localgroup administrators
net localgroup administrators usuario /add
```

---

## Red

```cmd
ipconfig /all
ping 8.8.8.8
tracert google.com
nslookup google.com
netstat -ano
route print
arp -a
```

---

## Disco

```cmd
chkdsk
diskpart
wmic logicaldisk get name,size,freespace
```

---

## Variables

```cmd
echo %USERNAME%
echo %COMPUTERNAME%
echo %USERPROFILE%
echo %PATH%
set VARIABLE=valor
```

---

## Ayuda

```cmd
comando /?
dir /?
ipconfig /?
net user /?
```
