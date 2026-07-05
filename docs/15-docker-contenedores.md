# 15 - Docker y contenedores

Docker permite ejecutar aplicaciones en contenedores: entornos aislados, reproducibles y fáciles de desplegar. En administración de sistemas es útil para laboratorios, despliegues, pruebas y servicios autocontenidos.

---

## 1. Conceptos esenciales

| Concepto | Explicación |
|---|---|
| Imagen | Plantilla de solo lectura para crear contenedores |
| Contenedor | Instancia en ejecución de una imagen |
| Dockerfile | Archivo que define cómo construir una imagen |
| Volumen | Almacenamiento persistente |
| Red Docker | Comunicación entre contenedores |
| Compose | Herramienta para definir varios servicios |
| Registry | Repositorio de imágenes |

---

## 2. Comandos básicos

```bash
docker version
docker info
docker images
docker ps
docker ps -a
docker pull nginx
docker run hello-world
```

---

## 3. Ejecutar contenedores

```bash
docker run nginx
docker run -d nginx
docker run -d --name web nginx
docker run -d -p 8080:80 nginx
docker stop web
docker start web
docker restart web
docker rm web
```

Opciones frecuentes:

| Opción | Uso |
|---|---|
| `-d` | Ejecutar en segundo plano |
| `--name` | Dar nombre al contenedor |
| `-p` | Publicar puerto |
| `-v` | Montar volumen o carpeta |
| `-e` | Variable de entorno |
| `--rm` | Eliminar al terminar |

---

## 4. Logs y acceso

```bash
docker logs contenedor
docker logs -f contenedor
docker exec -it contenedor sh
docker exec -it contenedor bash
docker inspect contenedor
```

---

## 5. Imágenes

```bash
docker images
docker pull imagen
docker rmi imagen
docker build -t mi-imagen .
docker history imagen
```

---

## 6. Dockerfile básico

```dockerfile
FROM debian:stable-slim

RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*

CMD ["bash"]
```

Construir:

```bash
docker build -t laboratorio-debian .
```

Ejecutar:

```bash
docker run -it laboratorio-debian
```

---

## 7. Volúmenes

Los contenedores son desechables. Para conservar datos se usan volúmenes.

```bash
docker volume create datos_app
docker volume ls
docker run -d -v datos_app:/datos --name app debian sleep infinity
```

Montar carpeta local:

```bash
docker run -v "$PWD":/trabajo debian ls /trabajo
```

---

## 8. Redes

```bash
docker network ls
docker network create red_lab
docker run -d --network red_lab --name contenedor1 nginx
```

Los contenedores en la misma red pueden comunicarse por nombre.

---

## 9. Docker Compose

Compose permite definir varios servicios en un archivo.

```yaml
services:
  web:
    image: nginx
    ports:
      - "8080:80"
```

Comandos:

```bash
docker compose up -d
docker compose ps
docker compose logs
docker compose down
```

---

## 10. Limpieza

```bash
docker system df
docker container prune
docker image prune
docker volume prune
docker system prune
```

Usar con cuidado: puede eliminar recursos no usados.

---

## 11. Buenas prácticas

- No guardar datos importantes solo dentro del contenedor.
- Usar volúmenes para datos persistentes.
- No meter secretos en imágenes.
- Usar `.dockerignore`.
- Mantener imágenes actualizadas.
- Documentar puertos y variables.
- Revisar logs.
- Usar Compose para entornos con varios servicios.

---

## 12. Checklist Docker

- [ ] Imagen identificada.
- [ ] Puertos documentados.
- [ ] Volúmenes definidos.
- [ ] Variables documentadas.
- [ ] Logs revisados.
- [ ] Datos persistentes fuera del contenedor.
- [ ] Limpieza controlada.
- [ ] Sin secretos en Dockerfile o Compose.
