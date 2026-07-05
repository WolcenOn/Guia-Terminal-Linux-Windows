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
| 1. Administración básica | Archivos, usuarios, permisos, procesos y servicios | [`docs/03-linux-administracion.md`](docs/03-linux-administracion.md), [`docs/04-windows-cmd-powershell.md`](docs/04-windows-cmd-powershell.md), [`docs/06-usuarios-permisos.md`](docs/06-usuarios-permisos.md), [`docs/07-procesos-servicios-logs.md`](docs/07-procesos-servicios-logs.md) |
| 2. Redes y servicios | IP, DNS, puertos, SSH, HTTP, firewall y diagnóstico | [`docs/05-redes-servicios.md`](docs/05-redes-servicios.md) |
| 3. Scripting | Bash, PowerShell y Python para automatizar tareas | [`docs/02-fundamentos-scripting.md`](docs/02-fundamentos-scripting.md), [`recursos/plantillas-scripts.md`](recursos/plantillas-scripts.md) |
| 4. ASIR avanzado | Bases de datos, seguridad, backups y alta disponibilidad | [`docs/08-backups-almacenamiento.md`](docs/08-backups-almacenamiento.md), [`docs/09-seguridad-hardening.md`](docs/09-seguridad-hardening.md), [`docs/10-bases-datos.md`](docs/10-bases-datos.md) |
| 5. Profesional | Monitorización, despliegue, Git, Docker, Ansible, documentación y proyectos | [`docs/12-automatizacion-profesional.md`](docs/12-automatizacion-profesional.md), [`docs/13-proyectos-practicos.md`](docs/13-proyectos-practicos.md), [`docs/14-git-github.md`](docs/14-git-github.md), [`docs/15-docker-contenedores.md`](docs/15-docker-contenedores.md), [`docs/16-monitorizacion.md`](docs/16-monitorizacion.md), [`docs/17-runbooks-incidencias.md`](docs/17-runbooks-incidencias.md), [`docs/18-ansible-iac.md`](docs/18-ansible-iac.md), [`docs/19-integracion-script-lab.md`](docs/19-integracion-script-lab.md) |

---

## Documentos principales

- [`docs/00-hoja-ruta.md`](docs/00-hoja-ruta.md): mapa completo para no dejar temas importantes fuera.
- [`docs/01-terminal-y-comandos.md`](docs/01-terminal-y-comandos.md): fundamentos de terminal, ayuda, sintaxis, rutas, tuberías y comandos base.
- [`docs/02-fundamentos-scripting.md`](docs/02-fundamentos-scripting.md): cómo se piensa y estructura un script útil.
- [`docs/03-linux-administracion.md`](docs/03-linux-administracion.md): administración Linux desde terminal.
- [`docs/04-windows-cmd-powershell.md`](docs/04-windows-cmd-powershell.md): administración Windows con CMD y PowerShell.
- [`docs/05-redes-servicios.md`](docs/05-redes-servicios.md): diagnóstico de red, puertos, DNS, SSH y firewall.
- [`docs/06-usuarios-permisos.md`](docs/06-usuarios-permisos.md): usuarios, grupos, permisos, sudo y ACL.
- [`docs/07-procesos-servicios-logs.md`](docs/07-procesos-servicios-logs.md): procesos, servicios, eventos y logs.
- [`docs/08-backups-almacenamiento.md`](docs/08-backups-almacenamiento.md): backups, restauración, almacenamiento y retención.
- [`docs/09-seguridad-hardening.md`](docs/09-seguridad-hardening.md): seguridad defensiva y endurecimiento inicial.
- [`docs/10-bases-datos.md`](docs/10-bases-datos.md): administración básica de bases de datos.
- [`docs/12-automatizacion-profesional.md`](docs/12-automatizacion-profesional.md): automatización con criterios profesionales.
- [`docs/13-proyectos-practicos.md`](docs/13-proyectos-practicos.md): proyectos para practicar y conectar con Script-Lab.
- [`docs/14-git-github.md`](docs/14-git-github.md): control de versiones aplicado a scripts y documentación.
- [`docs/15-docker-contenedores.md`](docs/15-docker-contenedores.md): contenedores, imágenes, volúmenes, redes y Compose.
- [`docs/16-monitorizacion.md`](docs/16-monitorizacion.md): métricas, logs, alertas y observabilidad.
- [`docs/17-runbooks-incidencias.md`](docs/17-runbooks-incidencias.md): procedimientos para diagnosticar y resolver incidencias.
- [`docs/18-ansible-iac.md`](docs/18-ansible-iac.md): Ansible e infraestructura como código.
- [`docs/19-integracion-script-lab.md`](docs/19-integracion-script-lab.md): conexión entre esta guía y Script-Lab.

---

## Cheatsheets

- [`cheatsheets/linux.md`](cheatsheets/linux.md)
- [`cheatsheets/windows-cmd.md`](cheatsheets/windows-cmd.md)
- [`cheatsheets/powershell.md`](cheatsheets/powershell.md)
- [`cheatsheets/python.md`](cheatsheets/python.md)
- [`cheatsheets/redes.md`](cheatsheets/redes.md)
- [`cheatsheets/git.md`](cheatsheets/git.md)
- [`cheatsheets/docker.md`](cheatsheets/docker.md)

---

## Recursos

- [`recursos/checklist-guia.md`](recursos/checklist-guia.md): checklist de contenidos.
- [`recursos/checklist-mantenimiento.md`](recursos/checklist-mantenimiento.md): checklist periódico de revisión de sistemas.
- [`recursos/ejercicios.md`](recursos/ejercicios.md): ejercicios progresivos por tema.
- [`recursos/glosario.md`](recursos/glosario.md): glosario de conceptos.
- [`recursos/plantillas-scripts.md`](recursos/plantillas-scripts.md): plantillas iniciales para Bash, PowerShell y Python.

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
├── cheatsheets/
├── scripts/
└── recursos/
```

---

## Pendiente próximo

- Completar aplicaciones web en un formato aceptado por el conector.
- Añadir ejercicios resueltos.
- Crear versiones ejecutables en Script-Lab.
- Añadir proyecto final completo de mantenimiento.

---

## Aviso

Muchos comandos pueden modificar usuarios, permisos, servicios, discos, redes o configuraciones críticas. Antes de ejecutar comandos destructivos, conviene entenderlos, probarlos en laboratorio y tener copias de seguridad.
