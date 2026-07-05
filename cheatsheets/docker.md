# Cheatsheet Docker

Referencia rápida de Docker y Docker Compose.

---

## Información

```bash
docker version
docker info
docker system df
```

---

## Imágenes

```bash
docker images
docker pull nginx
docker rmi imagen
docker build -t mi-imagen .
```

---

## Contenedores

```bash
docker ps
docker ps -a
docker run hello-world
docker run -d --name web nginx
docker run -d -p 8080:80 nginx
docker stop web
docker start web
docker restart web
docker rm web
```

---

## Logs y acceso

```bash
docker logs web
docker logs -f web
docker exec -it web sh
docker inspect web
```

---

## Volúmenes

```bash
docker volume ls
docker volume create datos
docker run -v datos:/datos debian
```

---

## Redes

```bash
docker network ls
docker network create red_lab
docker run --network red_lab nginx
```

---

## Compose

```bash
docker compose up -d
docker compose ps
docker compose logs
docker compose down
```

---

## Limpieza

```bash
docker container prune
docker image prune
docker volume prune
docker system prune
```
