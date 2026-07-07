# Actividades interactivas

Esta página agrupa actividades con preguntas desplegables, checklists y retos cortos. La idea es que el alumnado pueda autoevaluarse mientras estudia.

---

## 1. Autoevaluación de terminal

Marca lo que ya sabes hacer:

- [ ] Sé moverme entre carpetas.
- [ ] Distingo ruta absoluta y relativa.
- [ ] Sé consultar ayuda de un comando.
- [ ] Entiendo argumentos y opciones.
- [ ] Sé redirigir salida a un archivo.
- [ ] Sé usar tuberías.
- [ ] Sé interpretar errores básicos.

??? question "Pregunta 1: ¿Qué diferencia hay entre argumento y opción?"

    Una opción modifica el comportamiento del comando. Un argumento suele indicar sobre qué archivo, ruta, usuario, servicio o dato actúa el comando.

??? question "Pregunta 2: ¿Por qué no conviene copiar comandos sin entenderlos?"

    Porque algunos comandos pueden borrar archivos, cambiar permisos, modificar servicios o alterar configuraciones críticas.

---

## 2. Reto de Linux

!!! example "Reto"

    Crea una carpeta de laboratorio, genera tres archivos, lista su contenido, guarda el resultado en un archivo y busca una palabra dentro de ese listado.

??? success "Solución orientativa"

    ```bash
    mkdir laboratorio
    cd laboratorio
    touch uno.txt dos.txt tres.txt
    ls -lah > listado.txt
    grep "uno" listado.txt
    ```

---

## 3. Reto de PowerShell

!!! example "Reto"

    Obtén los diez procesos con mayor consumo de CPU y exporta el resultado a CSV.

??? success "Solución orientativa"

    ```powershell
    Get-Process | Sort-Object CPU -Descending | Select-Object -First 10 | Export-Csv procesos.csv -NoTypeInformation
    ```

---

## 4. Diagnóstico de red

Lee la situación y despliega la respuesta.

??? question "Caso: puedes hacer ping a 8.8.8.8 pero no a google.com. ¿Qué sospechas?"

    Probablemente hay un problema de DNS. La conectividad IP funciona, pero falla la resolución de nombres.

??? question "Caso: el servicio está activo pero el puerto no responde desde otro equipo. ¿Qué revisarías?"

    Revisaría si el servicio escucha en la IP correcta, si el firewall local permite el tráfico, si hay firewall intermedio y si el puerto publicado es el correcto.

---

## 5. Checklist antes de crear un script

- [ ] Sé qué problema resuelve.
- [ ] Sé qué entradas necesita.
- [ ] Sé qué salida debe producir.
- [ ] He probado los comandos manualmente.
- [ ] He pensado qué errores pueden ocurrir.
- [ ] He decidido si necesita logs.
- [ ] He decidido si necesita parámetros.
- [ ] He documentado un ejemplo de uso.

---

## 6. Detecta el riesgo

??? warning "Comando: eliminar una carpeta completa"

    Riesgo: pérdida de datos si la ruta es incorrecta. Antes de ejecutar, comprobar con `pwd`, listar la ruta y evitar variables vacías.

??? warning "Comando: cambiar permisos recursivamente"

    Riesgo: dejar datos expuestos o romper servicios. Antes de ejecutar, comprobar propietario, grupo, permisos actuales y alcance de la ruta.

??? warning "Comando: reiniciar un servicio"

    Riesgo: cortar un servicio usado por usuarios. Antes de ejecutar, comprobar impacto, horario, logs y procedimiento de vuelta atrás.

---

## 7. Mini evaluación

| Pregunta | Respuesta esperada |
|---|---|
| ¿Qué comando muestra puertos escuchando en Linux? | `ss -tulnp` |
| ¿Qué cmdlet prueba un puerto en PowerShell? | `Test-NetConnection` |
| ¿Qué herramienta versiona scripts? | Git |
| ¿Qué archivo suele ignorar archivos en Git? | `.gitignore` |
| ¿Qué herramienta define varios contenedores? | Docker Compose |

---

## 8. Siguiente paso

Cuando completes estas actividades, continúa con:

- [Ejercicios](../recursos/ejercicios.md)
- [Ejercicios resueltos](../recursos/ejercicios-resueltos.md)
- [Proyecto final](../proyectos/proyecto-final-mantenimiento.md)
