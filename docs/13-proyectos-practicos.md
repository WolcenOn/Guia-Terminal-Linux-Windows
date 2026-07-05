# 13 - Proyectos prácticos

Los proyectos prácticos convierten la guía en una herramienta real de aprendizaje. Cada proyecto debe combinar comandos, diagnóstico, documentación y scripting.

---

## Proyecto 1: inventario básico de sistema

### Objetivo

Crear scripts que recojan información del sistema y generen una salida clara.

### Debe incluir

- Nombre del equipo.
- Usuario actual.
- Sistema operativo.
- CPU.
- Memoria.
- Disco.
- IP.
- Fecha.

### Versiones

- Bash para Linux.
- PowerShell para Windows.
- Python multiplataforma.

---

## Proyecto 2: comprobador de servicios críticos

### Objetivo

Comprobar si una lista de servicios está activa.

### Debe incluir

- Lista configurable de servicios.
- Salida OK/ERROR.
- Código de salida.
- Log opcional.

### Ejemplos de servicios

Linux:

```text
ssh
cron
nginx
mysql
```

Windows:

```text
Spooler
WinRM
W3SVC
```

---

## Proyecto 3: monitor de espacio en disco

### Objetivo

Avisar cuando una partición o unidad supera un umbral de uso.

### Debe incluir

- Umbral configurable.
- Salida clara.
- Opción de guardar log.
- Posibilidad de programarse con cron o Task Scheduler.

---

## Proyecto 4: backup automatizado

### Objetivo

Crear copias de seguridad con fecha y retención.

### Debe incluir

- Ruta origen.
- Ruta destino.
- Fecha en el nombre.
- Compresión si aplica.
- Eliminación de backups antiguos.
- Log de ejecución.
- Prueba de restauración documentada.

---

## Proyecto 5: diagnóstico de red

### Objetivo

Automatizar una comprobación básica de conectividad.

### Debe incluir

- IP local.
- Gateway.
- Ping a gateway.
- Ping a IP externa.
- Resolución DNS.
- Prueba de puerto.
- Resultado final.

---

## Proyecto 6: revisión de logs

### Objetivo

Buscar errores recientes en logs del sistema o de una aplicación.

### Debe incluir

- Ruta o fuente de logs.
- Filtro por palabras clave.
- Número máximo de resultados.
- Exportación a archivo.

---

## Proyecto 7: auditoría básica de usuarios

### Objetivo

Listar usuarios, administradores y accesos recientes.

### Debe incluir

- Usuarios existentes.
- Grupos importantes.
- Administradores.
- Últimos accesos.
- Cuentas deshabilitadas si aplica.

---

## Proyecto 8: despliegue documentado de servicio

### Objetivo

Instalar, configurar, arrancar y verificar un servicio.

### Debe incluir

- Instalación.
- Configuración.
- Firewall.
- Servicio activo.
- Logs.
- Prueba de funcionamiento.
- Procedimiento de rollback.

---

## Proyecto 9: informe de mantenimiento

### Objetivo

Generar un informe con el estado de un sistema.

### Debe incluir

- Estado general.
- Disco.
- Memoria.
- Procesos principales.
- Servicios fallidos.
- Eventos o errores recientes.
- Recomendaciones.

---

## Proyecto 10: integración con Script-Lab

### Objetivo

Mover scripts maduros al repositorio Script-Lab o enlazarlos desde esta guía.

### Criterios para mover un script

- Tiene objetivo claro.
- Tiene parámetros.
- Tiene logs.
- Está probado.
- Está documentado.
- No contiene secretos.
- Tiene ejemplo de uso.

---

## Plantilla de documentación de proyecto

```text
Nombre del proyecto:
Objetivo:
Sistema compatible:
Requisitos:
Comandos utilizados:
Script principal:
Cómo ejecutarlo:
Salida esperada:
Errores comunes:
Cómo verificarlo:
Mejoras futuras:
```
