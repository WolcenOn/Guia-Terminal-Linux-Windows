# Guía Terminal Linux & Windows

Guía progresiva de terminal, comandos y scripting para administración de sistemas Linux y Windows.

Este repositorio nace como una referencia cómoda, práctica y pedagógica para estudiar, repasar y aplicar comandos reales de administración de sistemas. La idea es cubrir lo que se trabaja en ASIR, especialmente administración de sistemas, redes, servicios, seguridad, bases de datos, aplicaciones web, automatización y mantenimiento, y continuar después hacia un nivel profesional.

> Repositorio complementario futuro: [Script-Lab](https://github.com/WolcenOn/Script-Lab), pensado para scripts completos, prácticas y automatización avanzada.

---

## Objetivo

- Aprender a usar la terminal con criterio, no solo memorizar comandos.
- Comparar equivalencias entre Linux, Windows CMD y PowerShell.
- Crear una base sólida para scripting con Bash, PowerShell y Python.
- Documentar tareas reales de implantación, gestión y mantenimiento de sistemas.
- Construir una guía ampliable hasta un nivel profesional de administración de sistemas.

---

## Ruta de aprendizaje

| Nivel | Objetivo | Documentos |
|---|---|---|
| 0. Base | Entender la terminal, rutas, argumentos, tuberías y redirecciones | [`docs/00-hoja-ruta.md`](docs/00-hoja-ruta.md), [`docs/01-terminal-y-comandos.md`](docs/01-terminal-y-comandos.md) |
| 1. Administración básica | Archivos, usuarios, permisos, procesos y servicios | Próximamente |
| 2. Redes y servicios | IP, DNS, DHCP, HTTP, SSH, FTP, correo, firewall | Próximamente |
| 3. Scripting | Bash, PowerShell y Python para automatizar tareas | [`docs/02-fundamentos-scripting.md`](docs/02-fundamentos-scripting.md) |
| 4. ASIR avanzado | bases de datos, aplicaciones web, seguridad, alta disponibilidad | [`docs/00-hoja-ruta.md`](docs/00-hoja-ruta.md) |
| 5. Profesional | monitorización, hardening, backups, despliegue, Git, Docker, documentación | Próximamente |

---

## Primeros documentos

- [`docs/00-hoja-ruta.md`](docs/00-hoja-ruta.md): mapa completo para no dejar temas importantes fuera.
- [`docs/01-terminal-y-comandos.md`](docs/01-terminal-y-comandos.md): fundamentos de terminal, ayuda, sintaxis, rutas, tuberías y comandos base.
- [`docs/02-fundamentos-scripting.md`](docs/02-fundamentos-scripting.md): cómo se piensa y estructura un script útil.
- [`recursos/checklist-guia.md`](recursos/checklist-guia.md): checklist de contenidos que se irán completando.

---

## Filosofía de la guía

Cada tema debe intentar responder siempre a estas preguntas:

1. ¿Para qué sirve?
2. ¿Cuándo se usa en administración de sistemas?
3. ¿Cuál es la sintaxis básica?
4. ¿Qué opciones son las más importantes?
5. ¿Qué errores comunes hay que evitar?
6. ¿Cómo se automatiza con scripts?
7. ¿Cómo se documenta y verifica el resultado?

---

## Estructura prevista

```text
Guia-Terminal-Linux-Windows/
├── README.md
├── docs/
│   ├── 00-hoja-ruta.md
│   ├── 01-terminal-y-comandos.md
│   ├── 02-fundamentos-scripting.md
│   ├── 03-linux-administracion.md
│   ├── 04-windows-cmd-powershell.md
│   ├── 05-redes-servicios.md
│   ├── 06-usuarios-permisos.md
│   ├── 07-procesos-servicios-logs.md
│   ├── 08-backups-almacenamiento.md
│   ├── 09-seguridad-hardening.md
│   ├── 10-bases-datos.md
│   ├── 11-aplicaciones-web.md
│   ├── 12-automatizacion-profesional.md
│   └── 13-proyectos-practicos.md
├── cheatsheets/
│   ├── linux.md
│   ├── windows-cmd.md
│   ├── powershell.md
│   ├── python.md
│   ├── redes.md
│   ├── git.md
│   └── docker.md
├── scripts/
│   ├── bash/
│   ├── powershell/
│   └── python/
└── recursos/
    ├── checklist-guia.md
    ├── checklist-mantenimiento.md
    └── glosario.md
```

---

## Aviso

Muchos comandos pueden modificar usuarios, permisos, servicios, discos, redes o configuraciones críticas. Antes de ejecutar comandos destructivos, conviene entenderlos, probarlos en laboratorio y tener copias de seguridad.
