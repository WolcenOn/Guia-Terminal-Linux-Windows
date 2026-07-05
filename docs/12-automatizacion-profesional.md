# 12 - Automatización profesional

Automatizar no es solo escribir scripts. En un entorno profesional hay que crear procesos repetibles, seguros, documentados, versionados y verificables.

---

## 1. Objetivo

La automatización profesional busca:

- Reducir errores humanos.
- Ahorrar tiempo en tareas repetitivas.
- Ejecutar procedimientos iguales en varios sistemas.
- Registrar evidencias.
- Facilitar recuperación ante fallos.
- Mejorar mantenimiento y despliegue.

---

## 2. Niveles de automatización

| Nivel | Ejemplo |
|---|---|
| Comando manual | Ejecutar `df -h` |
| Script simple | Comprobar disco y mostrar alerta |
| Script parametrizable | Elegir ruta, umbral y salida |
| Script con logs | Guardar evidencias |
| Tarea programada | Ejecutar diariamente |
| Orquestación | Ejecutar en varios sistemas |
| CI/CD | Validar y desplegar automáticamente |

---

## 3. Buenas prácticas

- Usar control de versiones.
- Separar configuración y lógica.
- Validar parámetros.
- Controlar errores.
- Crear logs.
- Añadir modo de simulación.
- Documentar dependencias.
- Evitar credenciales en código.
- Probar en laboratorio.
- Crear procedimientos de restauración.

---

## 4. Git básico para scripts

```bash
git init
git status
git add .
git commit -m "Añade script de backup"
git branch
git checkout -b mejora-backup
git log --oneline
git diff
```

---

## 5. Estructura recomendada para scripts

```text
scripts/
├── bash/
│   ├── backup.sh
│   ├── comprobar_disco.sh
│   └── inventario.sh
├── powershell/
│   ├── backup.ps1
│   ├── inventario.ps1
│   └── revisar_eventos.ps1
└── python/
    ├── monitor_logs.py
    ├── comprobar_puertos.py
    └── generar_informe.py
```

---

## 6. Configuración externa

Evitar meter valores fijos dentro del script.

Mal:

```bash
DESTINO="/backups/servidor1"
```

Mejor:

```bash
DESTINO="${DESTINO:-/backups}"
```

En Python:

```python
import os

destino = os.getenv("DESTINO_BACKUP", "/backups")
```

---

## 7. Logs profesionales

Un log debería indicar:

- Fecha y hora.
- Nivel: INFO, WARNING, ERROR.
- Acción realizada.
- Resultado.
- Detalle del error si existe.

Ejemplo:

```text
2025-01-01 02:00:00 [INFO] Inicio backup
2025-01-01 02:01:12 [INFO] Backup creado correctamente
2025-01-01 02:01:13 [INFO] Fin
```

---

## 8. Tareas programadas

### Cron

```bash
crontab -e
```

```cron
0 2 * * * /home/admin/scripts/backup.sh >> /var/log/backup.log 2>&1
```

### PowerShell

```powershell
$Accion = New-ScheduledTaskAction -Execute "PowerShell.exe" -Argument "-File C:\Scripts\backup.ps1"
$Trigger = New-ScheduledTaskTrigger -Daily -At 02:00
Register-ScheduledTask -TaskName "BackupDiario" -Action $Accion -Trigger $Trigger
```

---

## 9. Documentación mínima de un script

Cada script debería documentar:

- Nombre.
- Objetivo.
- Sistema compatible.
- Requisitos.
- Parámetros.
- Ejemplos de uso.
- Salida esperada.
- Riesgos.
- Autor o responsable.
- Fecha de última revisión.

---

## 10. Plantilla de cabecera

```text
Nombre: backup.sh
Objetivo: crear copia de seguridad de una ruta.
Sistema: Linux.
Requisitos: tar, permisos de lectura sobre origen.
Uso: ./backup.sh /origen /destino
Riesgos: puede consumir espacio en disco.
```

---

## 11. Automatización con Python

Python es muy útil para:

- Leer archivos y logs.
- Generar CSV, JSON o informes.
- Conectar con APIs.
- Comprobar puertos.
- Analizar resultados.
- Crear herramientas multiplataforma.

Módulos frecuentes:

| Módulo | Uso |
|---|---|
| `os` | Variables de entorno y sistema |
| `pathlib` | Rutas y archivos |
| `subprocess` | Ejecutar comandos |
| `argparse` | Parámetros CLI |
| `logging` | Logs |
| `json` | Datos JSON |
| `csv` | Datos tabulares |
| `socket` | Red básica |

---

## 12. Checklist de automatización

- [ ] ¿La tarea merece automatizarse?
- [ ] ¿El script tiene objetivo claro?
- [ ] ¿Tiene parámetros?
- [ ] ¿Valida entradas?
- [ ] ¿Controla errores?
- [ ] ¿Registra logs?
- [ ] ¿Tiene modo simulación si modifica datos?
- [ ] ¿Está versionado con Git?
- [ ] ¿Tiene documentación?
- [ ] ¿Tiene prueba de restauración si afecta a backups?
