# 01 - Terminal y comandos

La terminal es una interfaz de texto para comunicarse con el sistema operativo. Permite ejecutar comandos, automatizar tareas, diagnosticar problemas y administrar sistemas de forma precisa.

---

## 1. Terminal, consola y shell

Aunque muchas veces se usan como sinónimos, no son exactamente lo mismo.

| Concepto | Explicación |
|---|---|
| Terminal | Programa donde escribes comandos |
| Consola | Interfaz de texto del sistema |
| Shell | Intérprete que entiende y ejecuta comandos |
| Bash | Shell común en Linux |
| CMD | Intérprete clásico de Windows |
| PowerShell | Shell moderno de Windows basado en objetos |

Ejemplos de shells:

```bash
bash
zsh
sh
```

```powershell
powershell
pwsh
cmd
```

---

## 2. Anatomía de un comando

Un comando suele tener esta estructura:

```text
comando [opciones] [argumentos]
```

Ejemplo en Linux:

```bash
ls -lah /etc
```

- `ls` es el comando.
- `-lah` son opciones.
- `/etc` es el argumento sobre el que actúa.

Ejemplo en PowerShell:

```powershell
Get-ChildItem -Path C:\Windows -Force
```

- `Get-ChildItem` es el cmdlet.
- `-Path` es un parámetro.
- `C:\Windows` es el valor del parámetro.
- `-Force` modifica el comportamiento.

---

## 3. Rutas absolutas y relativas

Una ruta indica dónde está un archivo o carpeta.

### Linux

```bash
/home/usuario/documentos     # Ruta absoluta
./script.sh                  # Ruta relativa al directorio actual
../backup                    # Directorio padre
```

### Windows

```powershell
C:\Users\Usuario\Documents   # Ruta absoluta
.\script.ps1                 # Ruta relativa
..\Backups                   # Directorio padre
```

---

## 4. Comandos básicos de navegación

| Acción | Linux | CMD | PowerShell |
|---|---|---|---|
| Ver ruta actual | `pwd` | `cd` | `Get-Location` |
| Listar archivos | `ls -lah` | `dir` | `Get-ChildItem` |
| Cambiar directorio | `cd /ruta` | `cd C:\ruta` | `Set-Location C:\ruta` |
| Crear carpeta | `mkdir carpeta` | `mkdir carpeta` | `New-Item carpeta -ItemType Directory` |
| Crear archivo vacío | `touch archivo` | `type nul > archivo` | `New-Item archivo -ItemType File` |
| Ver contenido | `cat archivo` | `type archivo` | `Get-Content archivo` |

---

## 5. Ayuda y documentación

Un administrador no memoriza todos los comandos. Aprende a consultar ayuda rápidamente.

### Linux

```bash
man ls
ls --help
apropos network
info coreutils
```

### Windows CMD

```cmd
dir /?
ipconfig /?
net user /?
```

### PowerShell

```powershell
Get-Help Get-Service
Get-Help Get-Service -Examples
Get-Command *Service*
Get-Member
```

---

## 6. Redirecciones

Las redirecciones permiten guardar la salida de un comando o controlar errores.

### Linux

```bash
ls > salida.txt              # Sobrescribe salida.txt
ls >> salida.txt             # Añade al final
comando 2> errores.txt       # Guarda errores
comando > salida.txt 2>&1    # Guarda salida y errores
```

### PowerShell

```powershell
Get-Process > procesos.txt
Get-Process >> procesos.txt
Get-Process 2> errores.txt
```

---

## 7. Tuberías

Una tubería envía la salida de un comando como entrada de otro.

### Linux

```bash
ps aux | grep nginx
cat /var/log/syslog | grep error
ls -lah | sort
```

### PowerShell

```powershell
Get-Process | Where-Object {$_.CPU -gt 100}
Get-Service | Where-Object {$_.Status -eq "Running"}
Get-ChildItem | Sort-Object Length -Descending
```

La diferencia importante es que PowerShell no pasa solo texto: pasa objetos. Por eso se pueden filtrar propiedades como `Status`, `CPU`, `Name` o `Length`.

---

## 8. Comodines

Los comodines permiten trabajar con patrones.

```bash
ls *.log
rm archivo?.txt
cp backup-2025-*.tar.gz /backups/
```

```powershell
Get-ChildItem *.log
Remove-Item archivo?.txt
Copy-Item backup-2025-*.zip C:\Backups
```

---

## 9. Variables de entorno

Las variables de entorno guardan información del sistema y de la sesión.

### Linux

```bash
echo $HOME
echo $USER
echo $PATH
env
export MI_VARIABLE="valor"
```

### Windows CMD

```cmd
echo %USERNAME%
echo %USERPROFILE%
echo %PATH%
set MI_VARIABLE=valor
```

### PowerShell

```powershell
$env:USERNAME
$env:USERPROFILE
$env:PATH
$env:MI_VARIABLE = "valor"
```

---

## 10. Códigos de salida

Cada comando devuelve un código de salida. Normalmente:

- `0` significa éxito.
- Otro valor significa error o resultado especial.

### Linux

```bash
ls /etc
echo $?
```

### PowerShell

```powershell
$LASTEXITCODE
$?
```

Esto es fundamental para scripting, porque permite tomar decisiones según si un comando ha funcionado o no.

---

## 11. Buenas prácticas

- Leer la ayuda antes de usar opciones destructivas.
- Usar rutas absolutas en scripts críticos.
- Probar primero con comandos de solo lectura.
- No copiar comandos de Internet sin entenderlos.
- Usar comillas cuando una ruta tenga espacios.
- Guardar evidencias en logs cuando se administran sistemas.
- Documentar comandos usados en incidencias reales.

---

## 12. Mini práctica

1. Crea una carpeta llamada `laboratorio-terminal`.
2. Entra en ella.
3. Crea tres archivos `.txt`.
4. Lista los archivos.
5. Guarda el listado en `salida.txt`.
6. Busca dentro de `salida.txt` una palabra concreta.
7. Elimina los archivos de prueba.

### Linux

```bash
mkdir laboratorio-terminal
cd laboratorio-terminal
touch uno.txt dos.txt tres.txt
ls -lah > salida.txt
grep "uno" salida.txt
rm uno.txt dos.txt tres.txt salida.txt
cd ..
rmdir laboratorio-terminal
```

### PowerShell

```powershell
New-Item laboratorio-terminal -ItemType Directory
Set-Location laboratorio-terminal
New-Item uno.txt, dos.txt, tres.txt -ItemType File
Get-ChildItem > salida.txt
Select-String "uno" salida.txt
Remove-Item uno.txt, dos.txt, tres.txt, salida.txt
Set-Location ..
Remove-Item laboratorio-terminal
```
