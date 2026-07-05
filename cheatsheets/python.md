# Cheatsheet Python para scripting

Referencia rápida de Python aplicado a administración de sistemas.

---

## Estructura base

```python
#!/usr/bin/env python3

def main():
    print("Inicio")

if __name__ == "__main__":
    main()
```

## Argumentos

```python
import argparse

parser = argparse.ArgumentParser(description="Script de ejemplo")
parser.add_argument("--ruta", default=".")
parser.add_argument("--dry-run", action="store_true")
args = parser.parse_args()
```

## Logs

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s [%(levelname)s] %(message)s"
)

logging.info("Mensaje informativo")
logging.warning("Aviso")
logging.error("Error")
```

## Archivos con pathlib

```python
from pathlib import Path

ruta = Path("archivo.txt")

if ruta.exists():
    print(ruta.read_text(encoding="utf-8"))
else:
    ruta.write_text("contenido", encoding="utf-8")
```

## Ejecutar comandos

```python
import subprocess

resultado = subprocess.run(
    ["whoami"],
    capture_output=True,
    text=True
)

print(resultado.stdout)
print(resultado.returncode)
```

## Variables de entorno

```python
import os

usuario = os.getenv("USER") or os.getenv("USERNAME")
print(usuario)
```

## JSON

```python
import json

datos = {"servicio": "ssh", "estado": "activo"}
texto = json.dumps(datos, indent=2)
print(texto)
```

## CSV

```python
import csv

with open("salida.csv", "w", newline="", encoding="utf-8") as archivo:
    writer = csv.writer(archivo)
    writer.writerow(["nombre", "estado"])
    writer.writerow(["ssh", "activo"])
```

## Red básica

```python
import socket

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.settimeout(2)
    abierto = s.connect_ex(("example.com", 443)) == 0
    print(abierto)
```

## Manejo de errores

```python
try:
    contenido = Path("archivo.txt").read_text(encoding="utf-8")
except FileNotFoundError:
    print("Archivo no encontrado")
except Exception as error:
    print(f"Error inesperado: {error}")
```
